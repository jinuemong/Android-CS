
## Content Provider 

- Activity, BroadcastReceiver, Service와 동일하게 안드로이드 애플리케이션을 구성하는 4대 컴포넌트
- 다른 애플리케이션의 데이터에 접근이 필요할 때 사용하는 컴포넌트
- 일반적으로 각 앱은 하나의 프로세스에서 실행되며, 자신의 프로세스에서 사하는 데이터는 자신만 접근 가능
- 사진첩, 연락처 정보들을 가져오기 위해서 ContentProvider 사용
- 앱의 보안을 위해 생겨난 안드로이드 기본 구성요소
- Manifest 파일에 명시해야 사용이 가능

### 특징

- 내 애플리케이션에서 다른 애플리케이션 엑세스
- 다른 애플리케이션과 데이터 공유
- ContentResolver 객체를 사용하여 ContentProvider와 서버- 클라이언트 구조로 통신
- ContentResolber 객체가 데이터를 요청하고, ContentProvider가 요청된 작업 실행 후 결과 반환
- CRUD 동작을 기본으로 사용하며, 데이터베이스, 파일 ,SharedPreference 3가지를 공유 

