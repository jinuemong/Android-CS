
## MVVM 패턴

- view, viewModel, Model을 분리
- 뷰와 모델간의 의존성 감소
- 화면 회전 등 뷰가 다시 생성되어도 뷰 모델을 통해 데이터 유지 가능

### 다른 패턴과의 차이

- MVC는 View와 Controller가 Activity에서 모두 처리 되어야 함
- Activity가 커지는 문제 발생

- MVP는 Presenter가 뷰와 1대1로 동작
- 프레젠터의 의존성이 강해지고, 로직이 비대해짐

