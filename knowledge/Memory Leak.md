

### 메모리 누수

- 앱을 일정시간 이상 사용하면 매우 느려져서 사용하기 힘들게 되는 경우 발생
- 메모리 관리에 실패한 경우
- 어느 영역에서 메모리 Leak이 발생하는지 확인하고, 관련 영역의 코드를 디버깅 해야함


### Profiler로 메모리 Leak 확인 

- CPU, 메모리, 네트워크 및 배터리 리소스 사용에 대한 실시간 데이터를 확인
- 메모리 누수가 일어날 것 같은 프로그램의 사용 시나리오를 생각하고, 해당 시나리오의 동작을 수행
- 하나의 참조를 다른 곳에서 유지하는 경우 시스템에서 가비지 컬렉션할 수 없음
- 가비지 컬터가 해당 객체를 여전히 필요한 객체라고 인식 
- Profiler를 통해 리소스 사용량과 누수를 확인 -> 추적하기 쉽지않다는 단점 


#### 참고 링크
- https://hodie.tistory.com/118#Memory%20Leak%EC%9D%B4%EB%9E%80%3F-1