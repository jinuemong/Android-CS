

## RESTful API

- 두 컴퓨터 시스템이 인터넷을 통해 정보를 안전하게 교환하기 위한 인터페이스
- 안전하고 신뢰할 수 있는 정보 교환을 지원 
- 서버와 클라이언트 구조
- GET,POST,PUT,DELETE 등의 메서드 사용 
- Request, Response로 이루어짐 

### 장점

- Open API를 제공하기 쉽다
- 멀티플랫폼 지원 및 연동이 용이하다
- 원하는 타입으로 데이터를 주고 받을 수 있다
- 기존 웹 인프라 (HTTP)를 그대로 사용할 수 있다

### 단점

- 사용가능한 메서드가 한정적
- 분산환경에는 부적합하며 HTTP 통신 모델에서만 지원한다 

### 안드로이드에서의 종류 
- HttpURLConnection
  - AsyncTask를 사용하여 구현
  - deprecated 되어 RxJava를 사용하여 비동기 처리 지원
- OkHttp
  - REST API, HTTP 통신을 간편하게 구현할 수 있도록 지원하는 java 라이브러리
  - Retrofit의 베이스 
- Retrofit
  - OkHttp 라이브러리의 상위 구현체
  - OkHttp 라이브러리를 네트워크 계층으로 활용하고 그 위에 구축

### 레트로핏의 구성요소

1. DTO
   - Data Transfer Object
   - JSON 타입 변환에 사용 됨
2. Interface
   - HTTP CRUD 동작 메소드 들을 정의해 놓은 인터페이스 
   - Create, Read, Update, Delete
3. Retrofit.Builder Class
   - Interface를 사용할 인스턴스, baseUrl, Converter를 설정

### put 과 patch의 차이 
- patch는 리소스에서 원하는 부분을 업데이트하는 것 
- put은 리소스의 모든 부분을 업데이트