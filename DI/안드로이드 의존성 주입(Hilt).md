

### 안드로이드에서 의존성 주입

- Dagger, Koin, Hilt

### Hilt
- Dagger2 기반 라이브러리
- Dagger보다 사용하기 쉽고 표준화된 사용법 제시
- 안드로이드 클래스에 최적화
- 프로젝트 규모에 따라서 안드로이드 클래스 외의 곳에 의존성 주입을 할 경우에는 단점으로 적용
- Hilt는 안드로이드가 클래스가 아니라면 부가적인 상용구가 필요
- Dagger는 동등한 방법으로 사용 가능 


### Hilt Component

- Hilt는 안드로이드 클래스에 대해서만 의존성 주입 
- @HiltAndroidApp : Application
- @HiltViewModel : ViewModel
- @AndroidEntryPoint : Activity, Fragment, View, Service, BroadcastReceiver


### Hilt Scope

- Hilt는 UnScoped 상태
- 앱이 객체를 요청할 때마다 새로운 객체가 만들어짐
- 이를 방지하고자 각 의존 객체는 Scope라는 이름의 생명주기를 지정
- 이 Scope의 범위를 나타내는 것이 Scope 어노테이션

> @Singleton : 앱 전체에 하나의 객체만 생성
> @ActivityScoped : Activity에 하나의 객체

- Component 종속 관계에 따라서 하위의 Component는 상위의 Scope를 가진 의존 객체에 접근 가능

### 바인딩
- 컴포넌트 안에 의존 객체와 의존 객체를 주입받을 객체를 연결하는 행위
- @Inject 어노테이션을 통해서 바인딩이 수행 됨
- 필드와 생성자에 대해서 의존성 주입을 할 수 있다

### 필드 주입 
- 주입받을 클래스에 @AndroidEntryPoint 어노테이션을 붙임
- 의존성을 제공받는 필드에 @Inject 어노테이션을 붙여서 바인딩 완료

 ```
 class AnalyticsAdapter @Inject constructor() { }

@AndriodEntryPoint
class ExampleActivity : AppCompatActivity() {
    
    @Inject 
    lateinit var analytics: AnalyticsAdapter
}
 ```

### 생성자 주입
- 의존 객체에 @Inject 어노테이션을 붙이고
- 주입 받을 클래스에 @AndroidEntryPoint 붙임
- @Inject constructor()를 통한 바인딩 

 ```
 class AnalyticsAdapter @Inject constructor() { }

@AndriodEntryPoint
class ExampleActivity @Inject constructor(
    val analytics: AnalyticsAdapter
) : AppCompatActivity() { }
 ```