

### LiveData

- 외부에서 데이터 읽기만 가능 


### MutableLiveData

- 외부에서 읽기, 쓰기 가능
- setValue() : UI 스레드에서만 동작 가능 , 화면 업데이트 
- postValue() : WorkThread, UI 스레드 둘다 가능
- -> 해당 함수를 호출하면 데이터를 메인 쓰레드로 보냄


### LiveData의 UI 업데이트 

- 기본적으로 LifecycleOwner 를 의존
- 데이터를 postValue or setValue 하면 해당 LiveData에서 데이터를 보관
- onStart, onResume 상태일 때 observe 함수를 호출한 곳에서 콜백을 받음
- LifeCycle에서 onDestroy 상태일 때 알아서 observe 호출 리스너를 제거 


### Recycler View에서 LiveData 처리

- ViewHolder에서 처리한다.

~~~
init {
	binding.setVariable(BR.vm, viewModel)
    itemView.doOnAttach {
    	binding.lifecycleOwner = ViewTreeLifecycleOwner.get(it)
    }

    itemView.doOnDetach {
    	binding.lifecycleOwner = null
    }
}
~~~


### List 형식을 LiveData에서 처리 

~~~
 private val _listTest : MutableLiveData<MutableList<String>> by lazy { MutableLiveData() }
 val listTest : LiveData<MutableList<String>> get() = _listTest
~~~

- 수정이 가능한 MutableLiveData를 private로 처리하여, 
- 뷰 모델 내부에서만 수정 가능하게 함
- LiveData는 사용자에게 노출 