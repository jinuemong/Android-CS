
### viewModel과 saveInstance의 차이점

- 뷰 모델은 화면이 돌아가거나 재생성되는 시기에 viewModel에서 데이터를 불러와 사용 가능하다.
- saveInstance에서도 해당 기능을 처리할 수 있으나, 해당 방식은 소형 데이터를 직렬화하거나 역 직렬화 하는데 적합하다.

### viewModel이 saveInstance를 완전히 대체할 수 없는 이유

- resource의 제약으로 activity가 강제로 꺼질 때 viewModel에서 문제가 발생한다.
- activity가 해당 동작으로 종료되면 다른 라이프 사이클 콜백의 호출 없이 바로 종료된다.
- 이 경우 viewModel에서는 데이터를 저장하지 못하는 경우가 발생.
- onStop에서 saveInstance는 정상 작동한다.
- 메모리가 부족해서 갑자기 종료되는 경우 onStop 상태에서 destory의 lifeCycle을 호출하지 않고 꺼질 수 있음

### viewModel을 사용하는 이유

- 화면 회전 등에 의해서 view가 다시 그려질 때, saveInstance는 메인 쓰레드에서 발생하기 때문에 시간과 리소스를 많이 소모
- saveInstance는 Bitmap과 같은 데이터를 담는 것을 권장하지 않음.
- viewModel의 경우 lifeCycle이 더 길기 때문에 대용량 데이터나 viewd와 로직 분리에 적절 