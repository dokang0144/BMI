# BMI
코틀린을 활용한 BMI 계산기
![image](https://user-images.githubusercontent.com/88234731/196194577-0ada46a5-edbd-4804-b245-391c12ad4f42.png)
## 실행화면
이름, 키, 몸무게를 입력하고 밑에 있는 버튼을 클릭하면 결과가 나옵니다.<br>
![제목 없음](https://user-images.githubusercontent.com/88234731/196195288-f4242b43-7305-4f0f-baee-162839a3e6f5.png)<br><br>
버튼을 클릭하면 **MainActivity**에서 입력받은 데이터를 **ResultActivity**로 보냅니다.
```kotlin
// MainActivity.kt
resultButton.setOnClickListener {
  val intent = Intent(this, ResultActivity::class.java) // 객체 생성
  intent.putExtra("name", nameEditText.text.toString()) // 데이터 추가
  intent.putExtra("height", heightEditText.text.toString().toInt())
  intent.putExtra("weight", weightEditText.text.toString().toInt())
  startActivity(intent) // 결과 인스턴스 시작
}
```
<br>

**ResultActivity**에서 데이터를 계산하고 결과를 별도의 화면에 출력합니다.
```kotlin
// ResultActivity.kt
override fun onCreate(savedInstanceState: Bundle?) {
  super.onCreate(savedInstanceState) // 인스턴스 불러오기
  setContentView(R.layout.activity_result) // 레이아웃 불러오기

  val name = intent.getStringExtra("name") // 변수 선언
  val height = intent.getIntExtra("height", 0)
  val weight = intent.getIntExtra("weight", 0)

  val bmi = weight / (height * 0.01).pow(2) // BMI 계산
  val resultText = when { // 결과
    bmi >= 30 -> "비만"
    bmi >= 25 -> "과체중"
    bmi >= 20 -> "정상"
    else -> "저체중"
  }

  val resultTextView: TextView = findViewById(R.id.resultTextView)
  resultTextView.text = "${name}님 BMI는 ${bmi}입니다. 결과는 ${resultText}입니다." // 결과 출력

  Toast.makeText(this,  "${name}/${height}/${weight}" , Toast.LENGTH_SHORT).show() // 토스트 메세지
}
```
