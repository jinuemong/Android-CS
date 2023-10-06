
## BaseActivity

- 개발 중 모든 액티비티에서 공통적으로 만들어주어야 하는 변수 발생
- 이 변수들을 파일마다 만들어주는 과정을 생략하기 위해서 Base 패키지에 필수적인 내용이 들어있는 파일 생성
- Activity 등에서 해당 파일을 상속해서 사용


### 특징
- abstract 추상 클래스로 정의
- abstract 정의 변수는 상속 받은 액티비티에서 재정의 해야 함
- 상속을 통한 구현 

### BaseViewModel
- BaseActivity 처럼 ViewModel에 필요한 변수와 함수를 정의
- 상속이 가능하도록 open 키워드 사용 