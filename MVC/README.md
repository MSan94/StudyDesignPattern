
# 2021.04.23 - Web이 아닌 Android에서의 MVC 패턴
- MVC 패턴이란?
  - Model, View, Controller의 약자
  - 하나의 애플리케이션, 프로젝트를 구성시 그 구성요소를 3가지로 구분한 패턴
![image](https://user-images.githubusercontent.com/81352078/115829239-b4ee0e00-a449-11eb-99b8-670a80fce5fe.png)

- 구성요소 3가지
  - Model
    - 애플리케이션의 사용되는 정보와 데이터 ( DB, 상수, 변수등..)
    - 위 데이터들의 가공을 책임지는 컴포넌트
    - 사용자가 편집하길 원하는 모든 데이터를 가져야 한다.
    - View, Controller에 대해 어떤 정보도 알지 않아야 한다.
    - 변경 발생 시 처리방법 구현
  - View
    - 데이터 및 객체의 입출력 담당
    - 사용자들이 볼 수 있는 화면
    - 모델이 가지고 있는 정보를 따로 저장하면 안된다.
    - 모델이나 컨트롤러와 같이 다른 구성요소들을 알면 안된다.
  - Controller
    - 데이터와 사용자 인터페이스 요소를 연결하는 다리 역활
    - 사용자의 이벤트를 처리하는 부분
    - 모델이나 뷰에 대해 알아야 한다
    - 모델과 뷰의 변경을 모니터링 해야 한다.
- 동작 순서
  - 안드로이드에서는 View와 Controller가 함께 공존
![image](https://user-images.githubusercontent.com/81352078/115830363-24183200-a44b-11eb-9844-417e4813ca69.png)
  - 안드로이드에서는 Class하나에 MVC가 처리 가능한 구조로 만들어 진다.
- 장점
  - 개발 단축
  - 코드 분석 용이
- 단점
  - 한 클래스의 코드 양 증가
  - 유지보수의 어려움
  - View와 Model의 결합도 상승
  - 테스트 코드 작성의 어려움
  - 복잡도 관리
- 예제 코드
```
<model>

data class UserData(
    var text : String
)
```
```
<controller>

class MainActivity : AppCompatActivity() {
    private val button : Button by lazy { findViewById(R.id.button) }
    private val button2 : Button by lazy { findViewById(R.id.button2) }
    lateinit var user : User
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener {
            user = User("Hello")
            Toast.makeText(this,"값 : ${user.text}" , Toast.LENGTH_SHORT).show()
            button.text = user.text
        }
        button2.setOnClickListener {
            user = User("goodbye")
            Toast.makeText(this,"값 : ${user.text}" , Toast.LENGTH_SHORT).show()
            button.text = user.text
        }
        
    }
}


```


![image](https://user-images.githubusercontent.com/81352078/117630720-6fa23e00-b1b6-11eb-83f7-68cc8e29a8bd.png)
