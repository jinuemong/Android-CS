

## RxJava vs Coroutine

### 차이
- RxJava는 Observable pattern으로 구독을 진행 -> 구독 후 들어오는 data를 stream 형태로 보냄
- RxJava는 중간에 변경되는 데이터를 stream을 통해서 확인 
- Coroutines는 함수 호출을 하고 return을 기다림 -> 리턴한 데이터로 다음 처리

### 공통점
- 둘 다 비동기 처리를 지원