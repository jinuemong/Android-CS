

## Flow
- Coroutines에 정식으로 추가 된 인터페이스
- RxJava의 Cold observable과 같은 기능을 함 
- Flow는 코루틴 상에서 스트림 작업 지원을 위한 구현체이다
- RxJava의 옵저버 기능을 지원
- 코루틴에서 데이터 스트림을 만들고 싶으면 사용하는 기능 
- suspend function을 보완하기 위해서 나옴 
- suspend function이 하나의 결과물을 던지면, 플로우를 이용하여 여러 개의 결과를 여러 형식으로 던짐

### 단점
- 화면 돌리기 등의 이벤트 발생 시 UI가 사용하는 데이터가 초기화되어 API 재요청 필요
- flow 데이터를 viewModel에 저장한 후, 이 데이터를 UI가 관찰
- 뷰 모델은 UI Controller 보다 수명 주기가 길기 때문에 flow가 끊겨도 UI가 데이터 유지
- 하지만 저장만을 위해서 데이터를 만드는 것은 비효율적인 보일러 플레이트 발생
- 위 단점을 해결하기 위해서 StateFlow 사용 

### Cold Flow, Hot Flow
- ColdFlow
  - Collector가 있을때만 데이터를 emit 할 수 있다. (emit : 방출)
  - 데이터를 저장하지 않음
  - 1:1 지원, 여러 개의 Collector를 가질 수 없음
- HotFlow
  - Collector가 없어도 데이터를 emit 할 수 있다
  - 데이터를 저장 할 수 없음
  - 1:N 지원, 여러 개의 콜랙터 가짐 

- ColdFlow : Flow, HotFlow : StateFlow, SharedFlow
[StateFlow, SharedFlow.md](StateFlow%2C%20SharedFlow.md)