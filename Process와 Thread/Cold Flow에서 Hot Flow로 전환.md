

### Cold Flow -> Hot Flow
- 뷰 모델에서는 Hot Flow를 사용자에게 더 노출해야 함
- 이유는 일반적인 flow 사용 시 새로운 구독을 할 때마다 Repository의 Flow Builder 블록에서
  Flow 방출을 트리거하여 리소스를 낭비할 수 있기 때문
- 보통 Repository로부터 전달된 Cold Flow를 Hot Flow인 State/SharedFlow로 변환
- 2가지 방법 사용
  - Flow를 수집 -> State/SharedFlow로 push
  - stateIn 확장 함수를 활용

### (1) 뷰 모델에서 Flow 수집

~~~
@HiltViewModel
class MyViewModel @Inject constructor(
  private val userRepository: UserRepository
) : ViewModel() {

  private val _userFlow = MutableStateFlow<UiState>(UiState.Loading)
  val userFlow: StateFlow<UiState> = _userFlow.asStateFlow()

  fun onRefresh() {
    viewModelScope.launch {
      userRepository
        .getUsers().asResult()
        .collect { result ->
          _userFlow.update {
            when (result) {
              is Result.Loading -> UiState.Loading
              is Result.Success -> UiState.Success(result.data)
              is Result.Error -> UiState.Error(result.exception)
            }
          }
        }
    }
  }
}
~~~
- UI State
~~~
sealed interface UiState {
  object Loading : UiState

  data class Success(
    val data: List<User>
  ) : UiState

  data class Error(
    val throwable: Throwable? = null
  ) : UiState
}
~~~
- Repository
~~~
interface UserRepository {
  fun getUsers(): Flow<List<User>>
}
~~~

### StateIn Flow Extension 활용

~~~
private const val DEFAULT_TIMEOUT = 5000L

@HiltViewModel
class MyViewModel @Inject constructor(
  userRepository: UserRepository
) : ViewModel() {

  val userFlow: StateFlow<UiState> = userRepository
    .getUsers()
    .asResult()
    .map { result ->
      when (result) {
        is Result.Loading -> UiState.Loading
        is Result.Success -> UiState.Success(result.data)
        is Result.Error -> UiState.Error(result.exception)
      }
    }
    .stateIn(
      scope = viewModelScope,
      initialValue = UiState.Loading,
      started = SharingStarted.WhileSubscribed(DEFAULT_TIMEOUT)
    )
}
~~~

- stateIn의 started 인자를 통해 구성 변경이 발생하는 경우 Flow 스트림이 다시 구독되지 않도록 보장
- DEFAULT_TIMEOUT으로 Google 샘플에서 권장하는 시간 제한 기본값을 적용
- stateIn 사용의 장점은 여러가지 Flow 들을 combine 할 수 있다는 장점을 가짐 
~~~
val uiState: StateFlow<HomeUiState> = combine(
    topRatedMovies,
    actionMovies
  ) { topRatedResult, actionMoviesResult ->

    val topRated: TopRatedMoviesUiState = when (topRatedResult) {
      is Result.Success -> TopRatedMoviesUiState.Success(topRatedResult.data)
      is Result.Loading -> TopRatedMoviesUiState.Loading
      is Result.Error -> TopRatedMoviesUiState.Error
    }

    val action: ActionMoviesUiState = when (actionMoviesResult) {
      is Result.Success -> ActionMoviesUiState.Success(actionMoviesResult.data)
      is Result.Loading -> ActionMoviesUiState.Loading
      is Result.Error -> ActionMoviesUiState.Error
    }

    HomeUiState(topRated, action)
  }
    .stateIn(
      scope = viewModelScope,
      started = WhileUiSubscribed,
      initialValue = HomeUiState(
        TopRatedMoviesUiState.Loading,
        ActionMoviesUiState.Loading
      )
    )
~~~
- 뷰 기반 프로젝트에서 State 수집
~~~
lifecycleScope.launch {
  lifecycle.repeatOnLifecycle(Lifecycle.State.STARTED) {
    viewModel.userFlow.collect {
      render(it)
    }
  }
}
~~~
- **lifecycle.repeatOnLifecycle(Lifecycle.State.STARTED)**
- 위 블록 안의 코드는 만약 라이프 사이클이 STARTED, STOPPED 사이에 있지 않다면 뷰 모델에서 Flow를 수집하지 않음
- 생명주기가 **started, resumed, paused** 상태인 경우만 데이터 수집
- 프래그먼트에서는 아래와 같이 사용
~~~
viewLifecycleOwner.lifecycleScope.launch {
  viewLifecycleOwner.repeatOnLifecycle(Lifecycle.State.STARTED) {
    viewModel.userFlow.collect {
      render(it)
    }
  }
}

private fun render(uiState: UiState) {
  when (uiState) {
    UiState.Loading -> TODO()
    is UiState.Success -> TODO()
    is UiState.Error -> TODO()
  }
}
~~~
- 프래그먼트는 viewLifeCycleOwner를 사용 

### Jetpack Compose 기반 프로젝트에서 State 수집
~~~
val uiState by viewModel.userFlow.collectAsStateWithLifecycle()
when (uiState) {
  UiState.Loading -> TODO()
  is UiState.Success -> TODO()
  is UiState.Error -> TODO()
}
~~~
- SharedFlow를 사용하는 경우
~~~
val uiState by shareInViewModel.userFlow.collectAsStateWithLifecycle(
  initialValue = UiState.Loading
)
~~~
- **collectAsStateWithLifecycle()**를 사용해서 
- hot flow(state/shared Flow)를 화면에 표시될 때만 수집
- 시스템 리소스 낭비 및 불필요한 네트워크 호출을 방지
- 이 방식은 LiveData와 비슷한 역할을 함 

-> 도메인 레이어에서 안드로이드 종속적인 LiveData를 사용하지 않고
-> 동일한 역할을 하는 StateFlow를 활용해서 클린 아키텍처 관점을 지킬 수 있음!