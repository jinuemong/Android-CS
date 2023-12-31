

### Context

- 추상 클래스로 Application 환경의 global한 정보에 접근하기 위한 인터페이스이다.
- 리소스, 데이터베이스, shared preference, 시스템 서비스 등에 접근하기 위해 사용할 수 있음
- 여러 컴포넌트들의 상위 클래스

### Application Context
- 싱글턴 인스턴스로 애플리케이션 라이프사이클에 묶여있음
- 애플리케이션이 살아있는 동안 변경되지 않는다.
- 현재 컨텍스트와 분리된 라이프사이클을 가진 컨텍스트가 필요할 때나 액티비티의 범위를 넘어선 컨텍스트를 전달할 때 사용
- 애플리케이션에서 싱글톤 객체를 생성할 경우 그 객체에 컨텍스트가 필요한 경우 사용 
  - 액티비티 컨텍스트를 전달할 경우 메모리 누수 발생
    - 액티비티는 가비지 콜렉터에 의해 수집되지 않으며, 액티비티에 대한 참조를 유지한다 

### Activity Context
- 액티비티 라이프사이클과 연결되어 있음
- 액티비티와 함께 소멸해야 하는 경우에 사용
- 액티비티 범위 내에서 컨텍스트를 전달한다
- GUI 작업에 주로 활용

### Application Context와 Activity Context

- 액티비티가 하는 일 모두를 애플리케이션 컨텍스트가 완전히 지원하지는 않는다.
- GUI 관련해서는 애플리케이션 컨텍스트를 활용하지 않는 것이 좋음 
  - ex> Dialog를 띄우는 작업은 애플리케이션 컨텍스트를 활용할 수 없음
  - GUI작업 중 유일하게 가능한 작업은 Toast 객체를 생성할 때이다.

### 적절한 사용 방법

- 엄지손가락의 법칙
  - 대부분의 경우 현재 작업중인 것을 둘러싸는 컴포넌트에서 직접 사용할 수 있는 컨텍스트를 사용
  - 참조가 해당 컴포넌트의 라이프사이클을 넘지 않는 이상 참조를 안전하게 유지
