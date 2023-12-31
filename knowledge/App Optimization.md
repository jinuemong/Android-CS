

## 앱 최적화 

- 사용자는 앱 시작부터 전체 앱 환경에 걸쳐 앱이 응답하고 빠르게 작동하기를 기대
- 앱에 성능 문제가 있는지 검사한 후 문제를 해결하고 성능 개선

### 도구 및 라이브러리
- 안드로이드는 가장 중요한 프로덕션 단계에서 앱 성능을 지속적으로 개선하기 위한 라이브러리 지원

### 성능 저하 요인 
- 많은 전력 사용
- 느리게 시작 (원하는 초기 화면 느리게 로드)
- 사용자 상호작용에 반응이 없거나 느린 반응
- ANR 등의 문제 

### 성능 개선 유형

- [레이아웃 성능 개선]
  - 레이아웃 계층 구조 최적화 
  - 실제 사용하는 타이밍에 뷰를 로드
- [스레딩을 통한 성능 개선]
  - 단일 스레드를 멀티 스레드로 구성
  - 코루틴과 같은 구조 설계
- [apk 사이즈 줄이기]
  - 린트 검사로 코드 개선
    - 코드에 구조적 문제가 없는지 확인
    - 지원 중단된 요소나 타겟 API에서 지원하지 안흔 호출 등
  - 사용하지 않는 라이브러리 및 코드, 리소스를 제거
  - ### 린트
    - 정적 코드 스캔 도구 
    - 앱을 실행하거나 테스트 사례를 작성할 필요 없이 코드의 구조적 품질 문제를 식별
- [메모리의 사이즈 최적화] 
  - 한정된 메모리안에서 앱이 원할히 동작하기 위해 메모리 확보 (가비지 컬렉션 지속적 구동)
  - 이는 결국 UI가 구동되어야 하는 시간과 겹치면서 사용자에게 버벅이는 화면 송출
  - 메모리 프로파일러를 활용할 수 있음
    - 메모리 할당을 추적하고 필요없는 객체를 사용하지 않게 수정 가능
  - #### 메모리 프로파일러
    - 끊김 현상, 멈춤, 앱 비정사 종료 등의 메모리 누수 및 변동을 식별 
    - 가비지 컬렉터가 사용되지 않는 메모리를 힙에 돌려보냄
    - 메모리 누수가 발생할 경우 앱이 백그라운드에 있는 동안에도 메모리를 유지할 수 있음
    - 이 동작으로 불필요한 가비지 컬렉션 이벤트가 강제 실행되여 메모리 성능 저하
  - onTrimMemory에 의해 메모리 부족 이벤트가 왔을 때 불필요한 객체들을 해제
- [기준 프로필 활용]
  - 일정 규칙을 만들고 적절히 사용하여 진입 성능 개선을 만들 수 있음
- [성능 프로파일 도구]
  - 성능 개선은 문제가 발생하는 원인이 어디에 기인하는지 확인이 우선
  - 안드로이드에서는 다양한 프로파일 & 디버깅 도구를 제공
  - 성능 이슈에 대한 정보를 획득하고, 옵션을 제공해야 함
- [다양한 프로파일러 활용]
  - 메모리 프로파일러 뿐 아니라 CPU, 메모리, 네트워크, 에너지 등 제공 
