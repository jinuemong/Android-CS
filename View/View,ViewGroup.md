

### View
- 뷰는 화면의 구성요소로 화면에 보여지는 모든 것이다
- 뷰에는 화면 어디에 배치 되어야 하는지에 대한 정보가 없기 때문에, 뷰만으로는 화면에 나타날 수 없음
- 따라서 뷰 그룹이 필요
- 안드로이드 화면에 보이는 각 요소들 
- 뷰 클래스를 상속받아 생성 됨

### ViewGroup
- 뷰 그룹은 뷰를 포함하여 화면에 적절히 배치하기 위한 일종의 컨테이너 
- 뷰들을 가지고 있으며, 레이아웃이라고 함
- 뷰 그룹은 뷰를 배치하고, 자식 뷰 그룹을 가질 수 있음
- 뷰 그룹 클래스를 상속받아 생성 됨
- ViewGroup 클래스는 View 클래스를 상속받고 있음 
- 뷰 그룹도 일종의 뷰 

![Untitled.png](..%2F..%2F..%2FDownloads%2FUntitled.png)
 
### 뷰의 종류
- TextView, EditText, Button, ImageView, CheckBox, RadioButton 등

### 뷰 그룹 종류

- LinearLayout : 내부 뷰들을 가로 또는 세로 방향 순서로 배치 
- FrameLayout : 내부 뷰들을 중첩하여 배치
- GridLayout : 내부 뷰들을 격자 형태로 배치 
- RelativeLayout : 내부 뷰들 간에 상대적인 위치에 따라 배치
- ConstraintLayout : 내부 뷰들의 크기와 위치를 다른 요소들과의 제약조건을 설정하여 배치
- TableLayout : 내부 뷰들을 행과 열의 표 형태로 배치 