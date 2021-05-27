```💡 FastCampus 강의 수강 및 정리```

### Voice_Recoder
+ Request runtime permissions(위험권한 : 마이크접근)  
  권장되는 순서는 공식홈페이지에 나와있음(무조건적인건 아님!)
+ external storage(위험권한 : 저장소)
+ Custom View(Custom Drawing : 음성 시각화 canvas, onDraw) // 반복하기
+ MediaRecorder(음성 녹음)

### check list
+ enum class
+ companion object : java에서 static 느낌?? 동작방식을 그렇게 보이지만 차이가 있음  
  객체이다
+ set(value) {  
  field = value  
  ...  
  }


### Step
1. 녹음 전 👉 2. 녹음 중 👉 3. 녹음 후 👉 4. 재생 중  

기본적인 순서는 위와 같이 구성하며, [4.재생 중]일 때 "정지" 버튼을 누르면 [3.녹음 후] 돌아갈 수 있도록하고 "Reset" 버튼을 누르면 [1.녹음 전] 으로 돌아갈 수 있도록 한다.


<img src="https://user-images.githubusercontent.com/63087903/119835634-f76ca400-bf3b-11eb-85d3-461f27a1e588.jpg" width="200" height="430"> <img src="https://user-images.githubusercontent.com/63087903/119835628-f63b7700-bf3b-11eb-8a89-12073bdc68cc.jpg" width="200" height="430">

## [2021-05-12]

### Custom UI 그리기
1. View Class 만들기 [👉](https://developer.android.com/training/custom-views/create-view?hl=ko)
  ```KOTLIN
  // activity_main.xml
    
  <com.com.voicerecoder.SoundVisualizerView ... />
  <com.com.voicerecoder.CountUpView ... />
  <com.com.voicerecoder.RecordButton ... />
  ```
  각 뷰에해당하는 클래스 파일들을 생성
  ```KOTLIN
  // kotlin.kt
  
  SoundVisualizerView.kt
  CountUpView.kt
  RecordButton.kt
  ```
2. Custom View 만들기 [👉](https://developer.android.com/training/custom-views/custom-drawing?hl=ko)  
  전반적으로 익숙치 않아서 어려움 (음성파일 > 이미지시각화 하는 부분 : Visualizer)  
  공식문서 참고하고 코드참조해보면서 복습할것
  
### 권한부여하기 > [👉](https://developer.android.com/training/permissions/requesting?hl=ko#allow-system-manage-request-code)
권한을 부여하는 부분은 딱히 코드상 생각하고 구현해야한다기 보다 공식문서 순서를 그대로 따르기 때문에  
문서를 참조하는게 좋을듯함 

💡 data class, inner class, enum class 등 코틀린의 여러가지 클래스  
💡 .firstOrNull() ??, attr ??  
💡 companion object [👉](https://www.bsidesoft.com/8187)  
  const val ?
