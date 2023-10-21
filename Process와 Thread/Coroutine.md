

## 코루틴

- 일시 중단이 가능한 (Suspendable) 작업 객체
- 동시성을 보장하는 쓰레드와 비슷한 개념을 가짐
- 하지만 어떤 쓰레드에도 종속되지 않는다는 특징
- 한 코루틴 작업을 여러 쓰레드를 왔다갔다 하며 실행할 수도 있음 
- 경량 쓰레드라고 함
- 실제 사용법은 다름 

### 코루틴 예제
~~~
import kotlinx.coroutines.delay
import kotlinx.coroutines.launch
import kotlinx.coroutines.runBlocking

fun main() = runBlocking {  // Coroutine Scope
    launch {  // 새로운 코루틴 객체를 생성 & 해당 코루틴 동작 시작
        delay(1000L)  // Non-blocking 1초 딜레이 커맨드
        println("World!")  // 1초 후에 출력됨!
    }
    println("Hello!")  // Main Coroutine 은 delay 되지 않고 이어서 수행됨
}

// [실행결과]
// Hello
// World!
~~~

### launch 키워드
- 코루틴을 만드는 Coroutine Builder
- 다른 코드들과 동시에, 독립적으로 동작하는 코루틴 객체를 생성한다
- 코루틴이 속한 쓰레드를 블로킹하지 않는다 (독립적 실행의 개념)
- 위 예시에서 launch 스코프에 딜레이를 줬기 때문에 Hello가 먼저 출력된다.

### delay 키워드
- 특별한 **Suspending** (일시 중단) 함수이다.
- 해당 코루틴을 특정 시간동안 일시 중단하는 기능을 수행한다
- 속해있는 쓰레드가 통째로 Bloacking 되는 것은 아니고, 일시 중단되는 동안 다른 코루틴이 동작한다.

### runBlocking
- 코루틴 객체를 만드는 행위
- 코루틴 요소가 포함되지 않는 일반적인 코드 블럭과 이 runBlocking 스코프 내의 코루틴 
  동작 코드 블럭들을 이어줌
- Coroutine Scope 영역이라고 함 
- launch 키워드는 코루틴 객체를 생성하므로 반드시 runBlocking 스코프 내부에 선언해야 함
- runBlocking 사용 시 이것이 속한 쓰레드를 해당 스코프 내의 모든 코루틴 동작들의 실행이 완료 될 때까지
  블로킹 한다는 뜻을 가짐위


### 프로덕션 코드에서의 runBlocking
- 실제 프로덕션 코드에서는 거의 사용하지 않음
- 쓰레드는 고비용 리소스이고 이를 블로킹하는 것은 매우 비효율적종
- 테스트 코드에서 종종 사용

### 코루틴의 구조화된 동시성 원칙
- 새로운 코투린 객체는 반드시 코루틴의 수명을 제한하는 특정 코루틴 스코프 내에서 실행해야 함
- runBlocking이 그 역할을 함 
- 코루틴이 각각 손실되지 않는 것을 보장 
- 각 코루틴 스코프는 스코프 내의 하위 코루틴들 각각이 모두 완료될 때까지 종료될 수 없다는 특징 