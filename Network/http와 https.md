
### http

- 서버, 클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜
- 암호화가 되지 않은 평문 데이터 전송 -> 보안에 취약

### https

- 기존 http에 데이터 암호화가 추가 된 프로토콜
- 보안에 취약한 http의 약점을 보완
- post, get, put, patch, delete 연산

### https 요청 인자

- Field: @FormUrlEncoded 어노테이션을 사용해서 전달
  - key - value 형식
- Body : Json 형태의 하나의 객체만 전달 (key: value)
- Query: Query Parameter를 명시
  - URL 뒤에 전달되어야 하는 key-value 형식의 파라미터 GET /users?id=123&pw=***
  - 끝에는 ? 추가 됨, 경로 및 파라미터를 구분하는 기준 
- Path : 쿼리와 다르게 경로 자체를 변수로써 활용 GET /users/123