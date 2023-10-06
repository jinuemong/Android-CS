

## 클로저

- 상위 함수 영역의 변수를 접근할 수 있는 함수
- () -> Unit
- 익명함수는 함수 밖에서 정의 된 변수에 접근 가능 
- 내부 함수에서 외부 함수의 데이털르 사용할 경우, 외부 함수의 코드블럭이 끝나도 내부 함수에서 참조하는 변수는 계속 살아남아 있는 현상
- 어떤 변수를 전역변수처럼 쓰고싶은데 노출하기 싫은경우 

~~~
fun add(x: Int): (Int) -> Int {
    return fun(y: Int): Int {
        return x + y
    }
}

fun main(args: Array<String>) {
    val func = add(10)
    val result = func(20)
    println(result)
}
~~~