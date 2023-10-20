

## StateFlow, SharedFlow
- 두가지 모두 Flow에서 최적으로 데이터 state 업데이트를 내보냄
- 여러 소비자에게 값을 내보낼 수 있음

### StateFlow
- Observable flow
- State를 지니고 있음
- 최신 및 새로운 상태를 여러 collectors에게 업데이트 시켜줌
- value property를 통해 값을 받을 수 있음
- state를 업데이트하고 flow로 보내려면 MutableStateFlow 클래스의 value 속성에 값 할당
- flow를 StateFlow로 변환하려면 stateIn 중간 연산자 사용 
- SharedFlow의 구체화 버전 
- 더 효율적이고 API 간단, 상태 관리에 잘어울림 (ViewModel과 사용 )
~~~
class LatestNewsViewModel(
    private val newsRepository: NewsRepository
) : ViewModel() {

    private val _uiState = MutableStateFlow(LatestNewsUiState.Success(emptyList()))
    val uiState: StateFlow<LatestNewsUiState> = _uiState

    init {
        viewModelScope.launch {
            newsRepository.favoriteLatestNews
                // 최신뉴스를 통해 view 업데이트
                // value에 값을 할당 하면 flow에 새로운 요소가 추가되고 
                // 이 flow를 수집하는 모든곳이 업데이트 된다.  
                .collect { favoriteNews ->
                    _uiState.value = LatestNewsUiState.Success(favoriteNews)
                }
        }
    }
}

// 최신뉴스 화면에 서로 다른 상태 값
sealed class LatestNewsUiState {
    data class Success(news: List<ArticleHeadline>): LatestNewsUiState()
    data class Error(exception: Throwable): LatestNewsUiState()
}
~~~
- 관찰이 필요한 가변상태를 유지해야하는 클래스에 적합
- API 요청(생산자)으로 MutableStateFlow를 업데이트
- 데이터 사용 객체(소비자)가 stateFlow를 수집 
- HotFlow 사용 (flow를 수집하는 쪽이 생산자 코드를 실행하지 않음 )
- **상태가 변하는 값을 읽거나, 네트워크 상태 정보 값을 읽을 때 사용**
- LiveData와 Observable data holder 클래스를 사용하는 유사성이 있음

### LiveData와 다른점?
- StateFlow를 생성할 때 생성자에 전달되는 초기 state가 필요, LiveData는 필요 없음
- LiveData.observe()는 View가 stopped 상태가 될 대 자동으로 소비자를 등록 해제
- StateFlow, Flow는 collecting 하는 것으로 이를 방지 (따라서 UI 계층에서 collection 사용 금지)
- HotFlow 구현에서 UI가 화면에 표시되지 않을 때 (백그라운드) collecting 사용에 주의해야 함
- 리소스 낭비가 될 수 있으며, 흐름 수집을 수동으로 중지해야 함 
~~~
class LatestNewsActivity : AppCompatActivity() {
    ...
    // UI states를 위한 참조
    private var uiStateJob: Job? = null

    override fun onStart() {
        super.onStart()
        // view 가 가시상태면 수집 시작한다. 
        uiStateJob = lifecycleScope.launch {
            latestNewsViewModel.uiState.collect { uiState -> ... }
        }
    }

    override fun onStop() {
        // view 가 보이지 않으면 collecting을 멈춘다.
        uiStateJob?.cancel()
        super.onStop()
    }
}
~~~

### SharedFlow
- Cold Flow, Cold Stream(일반 Flow)의 진화 버전, 여기서 State Flow로 변환 가능
- 하나의 소비자에게 값을 보냄
- 생성된 이후 누군가 소비를 시작하면 데이터 발행
- 이벤트 핸들링에 적합 
- StateFlow의 일반화 버전
- 시간이 지남에 따라 동일한 이벤트를 트기러 해야하는 경우 (ex> SnackBar, 탐색, 네트워크 연결 상태)
- 동일한 값을 재방출 하는 방식으로 진행
- ViewModel의 init 블록 안에서 SharedFlow를 푸시, collector가 아직 수집을 하지 않은 경우 
  collector가 해당 방출을 놓칠 수 있음

