

### ListView

- 최초 생성이나 스크롤 시 아이템을 생성할 때마다 뷰 바인딩
- 성능 저하 위험이 있음

### RecyclerView

- ViewHolder 패턴을 강제로 구현하게 해서 뷰 바인딩을 한 번만 함
- 아이템을 생성할 때 바인딩된 뷰 객체를 재활용함

### 뷰 바인딩
- 뷰와 상호작용하는 코드를 쉽게 작성하기 위해 사용
- 각 XML 레이아웃 파일에 대한 바인딩 클래스가 자동으로 생성

### findViewById

- XML의 뷰와 변수를 연결하여 사용
- 여러러 문제점이 발생 → view Binding으로 대체
    - Null에 안전하지 않음
    - Type에 안전하지 않음
    - 런타임 오류와 속도, 코드 문제
    - → 코드가 일치하지 않는 경우 발생, 바인딩 코드 길어짐, 속도 증가

### View Holder

- View를 보관하는 객체
- ListView와 RecyclerView는 inflate를 최소화하기 위해 View를 재활용
- 성능 저하 방지를 위한 각 item 요소를 바로 엑세스 할 수 있도록 저장해두고 사용