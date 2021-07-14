```💡 FastCampus 강의 수강 및 정리```

### Voice_Recoder
+ Request runtime permissions(위험권한 : 마이크접근 / 마이크 권한 런타임에 얻기)  
  권장되는 순서는 공식홈페이지에 나와있음(무조건적인건 아님!)
+ external storage(위험권한 : 저장소)
+ Custom View(Custom Drawing : 음성 시각화 canvas, onDraw)
+ MediaRecorder(녹음)
+ MediaPlayer(재생)

### Step
1. 녹음 전 👉 2. 녹음 중 👉 3. 녹음 후 👉 4. 재생 중  

기본적인 순서는 위와 같이 구성하며, [4.재생 중]일 때 "정지" 버튼을 누르면 [3.녹음 후] 돌아갈 수 있도록하고 "Reset" 버튼을 누르면 [1.녹음 전] 으로 돌아갈 수 있도록 한다.


<img src="https://user-images.githubusercontent.com/63087903/119835634-f76ca400-bf3b-11eb-85d3-461f27a1e588.jpg" width="200" height="430"> <img src="https://user-images.githubusercontent.com/63087903/119835628-f63b7700-bf3b-11eb-8a89-12073bdc68cc.jpg" width="200" height="430">

### [2021-05-12]
### [2021-07-14 ing~~]

#### manifest
+ 오디오 녹음기능과, 외부 저장소 접근 권한 추가
  ```KOTLIN
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
  ```

#### layout.xml
+ activity_main 에 Custom UI를 그리기 위한 View Class 만들기 [👉](https://developer.android.com/training/custom-views/create-view?hl=ko)
  ```KOTLIN
  // activity_main.xml
    
  <com.com.voicerecoder.SoundVisualizerView ... />
  <com.com.voicerecoder.CountUpView ... />
  <com.com.voicerecoder.RecordButton ... />

  // kotlin.kt
  
  SoundVisualizerView.kt
  CountUpView.kt
  RecordButton.kt
  
  * 각 뷰에해당하는 클래스 파일들을 생성
  ```
+ Custom Drawing [👉](https://developer.android.com/training/custom-views/custom-drawing?hl=ko)  
  record 로 저장한 녹음 파일 > 이미지 시각화 하는 부분 : Visualizer
  ```KOTLIN
  * SoundVisualizerView.kt
  ```
  
### 권한부여하기 > [👉](https://developer.android.com/training/permissions/requesting?hl=ko#allow-system-manage-request-code)
권한을 부여하는 부분은 딱히 코드상 생각하고 구현해야한다기 보다 공식문서 순서를 그대로 따르기 때문에  
문서를 참조하는게 좋을듯함 

💡 data class, inner class, enum class 등 코틀린의 여러가지 클래스  
💡 .firstOrNull() ??, attr ??  
💡 companion object [👉](https://www.bsidesoft.com/8187)  
   ```KOTLIN
   Java에서 static 사용하는 느낌?? 동작방식은 static 같이 보이지만 엄연한 차이가 존재하긴함
   
   이전 프로젝트인 timer 에서도 object객체생성에 대한 부분이 나왔던거 같은데
   확실하게 체크하기
   ```
💡 const val  
💡 set(value) {  
   field = value  
   ...  
   }

