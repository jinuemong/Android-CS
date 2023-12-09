

## OKHttp3

- Square 사의 Open Source 라이브러리로 HTTP 통신에 사용
- GET,PUT,POST 등을 쉽게 구현할 수 있도록 도움 
- 안드로이드 쪽에서 클라이언트 역할을 하면 OKHttp3는 서버와의 네트워크 통신을 구현

### 장점

- 네트워크 통신은 Worker Thread에서 동작
- 이전에는 HttpUrlConnectioon, Async Task 등을 이용하여 구현
- OkHttp3를 통해서 네트워크 통신을 매우 간단하게 구현 
- RESTful API를 다루는 Retrofit2와 같이 사용됨 

### Retrofit2

- Square 사의 라이브러리로, RESTful 한 인터페이스를 가지는 CRUD 방식의 서버 연결을 쉽게 제공