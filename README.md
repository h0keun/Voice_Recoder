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
2. Custom View 만들기 [👉](https://developer.android.com/guide/topics/ui/custom-components?hl=ko)



💡 data class, inner class, enum class 등 코틀린의 여러가지 클래스 
💡 .firstOrNull() ??, attr ??
💡 companion object [👉](https://www.bsidesoft.com/8187)
