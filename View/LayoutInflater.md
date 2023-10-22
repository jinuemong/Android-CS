
## LayoutInflater
- xml에 정의된 리소스를 view 객체로 반환하는 역할을 함
- onCreate() setContentView() 또한 inflater 역할
- 위 함수 내부에서 LayoutInflater가 실행되어 view를 객체화 

### inflate() 함수의 3가지 인자
- 객체화하고자 하는 xml 뷰 파일
- 객처화 된 뷰를 붙일 부모의 레이아웃이나 컨테이너
- Boolean 값 (true : 부모 view에 바로 붙임, false : 나중에 붙이기)
