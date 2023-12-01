
### MVVM 패턴
- view, viewModel, Model을 분리하여 뷰와 모델간의 의존성을 감소시킵니다.
- #### 다른 패턴과의 차이
  - MVC는 View와 컨트롤러가 모두 액티비티에서 처리되어야 하기 때문에 액티비티가 커지는 문제 발생 합니다.
  - MVP는 Presenter가 뷰와 1대1로 동작하면 프레젠터의 의존성이 강해져서 로직이 비대하다는 단점이 있습니다.

### MVVM ViewModel과 AAC ViewModel
- MVVM에서는 View와 Model 사이에서 데이터를 관리해주고 바인딩하는 역할을 합니다.
- AAC에서는 화면 회전 같은 환경에서 데이터를 보관하고, 액티비티나 프래그먼트 Destory시 onClear() 함수를 통한 데이터의 해제 역할을 함
- AAC는 액티비티 내에서 1개만 생성 가능하며, 싱글톤의 개념을 가집니다.

### LiveData
- 데이터의 변경을 관찰할 수 있는 데이터 홀더 클래스로 외부에서 데이터 읽기만 가능합니다.

### MutableLiveData
- 외부에서 읽기, 쓰기 가능하며 setValue, postValue 함수 사용이 가능합니다.
- setValue는 UI 스레드에서만 동작 가능하며, postValue는 모든 스레드에서 사용 가능합니다.
- postValue를 통해서 함수를 호출하면 데이터를 메인 스레드로 보내줍니다.

### LiveData의 UI 업데이트
- 기본적으로 LifecycleOwner를 의존하며 post,setvalue로 Livedata에서 데이터를 보관합니다.
- onstart, onresume 상태일 때 옵저버 함수를 호출한 곳에서 콜백을 받습니다.
- 라이프 사이클이 onDestory 상태가 되면 알아서 옵저버를 호출하는 리스너를 제거합니다.

### LiveData 처리
- 수정이 가능한 MutableLiveData를 private로 처리, 뷰 모델 내부에서만 수정 가능하게 합니다.
- LiveData는 수정이 불가능하므로 사용자에게 노출합니다.