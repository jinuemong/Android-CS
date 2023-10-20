

## Rxjava

- 함수형 프로그래밍을 통한 비동기 데이터 흐름에 중점을 둠
- 반응형 프로그래밍을 쉽게 적용할 수 있도록 도와주는 라이브러리
[함수형 프로그래밍.md](%ED%95%A8%EC%88%98%ED%98%95%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D.md)
[반응형 프로그래밍.md](%EB%B0%98%EC%9D%91%ED%98%95%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D.md)

### ReactiveX
- 반응을 확장
- 옵저버르 스트림으로 비동기 프로그램이을 하기 위한 API
- 다양한 시리즈가 있으며, 안드로이드, IOS 등 어느 플랫폼에서나 사용 가능
- 여기서 가장 대표적으로 사용하는게 RxJava를 사용

### Rx 예시
~~~
import RxSwift
 
let disposeBag = DisposeBag()
 
let value = ["물고기", "쓰레기"] // 강에 흐르는 value
let rx = Observable.from(value) // Observable: value가 흐르는 'rx'강
    
rx
    .filter { $0 == "물고기" } // Operators: 물고기만 건짐
    .map { "\($0) 회" } // Operators: 물고기를 회로 만듦
    .subscribe { print($0.element ?? "") } // Subscribe: 'rx'강을 구독
    .disposed(by: disposeBag)
~~~
- rx라는 옵저버를을 통해서 구독한 다음 값을 얻음

