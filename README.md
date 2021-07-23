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
### [2021-07-23 ing~~]

#### manifest
+ 오디오 녹음기능과, 외부 저장소 접근 권한 추가
  ```KOTLIN
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
  ```
+ MainActivity.kt
  ```KOTLIN
  * 요청할 권한들을 담을 배열에 음성 녹은 관련 권한을 담아준다.
    (이렇게 하는 이유는 보통 규모가 있는 앱에서는 단일권한이 아니라 여러 권한을 받아오기 때문에 배열에 담는다... 
    고 생각했었는데 애초에 requestPermissions 메서드가 받는 파라미터가 배열값임) 
    
  private val requiredPermissions = arrayOf(
      android.Manifest.permission.RECORD_AUDIO,
      android.Manifest.permission.READ_EXTERNAL_STORAGE
  )
    
  * onCreate() 에서 requestAudioPermission() 함수를 호출하고 함수 내부에서
    requestPermissions 메서드 호출(파라미터로 권한을 담은 배열과, 리퀘스트 코드번호가 주어짐)
    권한 요청에 따른 사용자의 답변은 onRequestPermissionsResult를 재정의 함으로서 처리한다.
  
  private fun requestAudioPermission(){
      requestPermissions(requiredPermissions, REQUEST_RECORD_AUDIO_PERMISSION)
  } 
  
  // REQUEST_RECORD_AUDIO_PERMISSION 는 companion object로 선언한 상수값 201 이다.

  * onRequestPermmisionsResult

  override fun onRequestPermissionsResult(
      requestCode: Int,
      permissions: Array<out String>,
      grantResults: IntArray
  ) {
      super.onRequestPermissionsResult(requestCode, permissions, grantResults)

      val audioRecordPermissionGranted =
          requestCode == REQUEST_RECORD_AUDIO_PERMISSION &&
                  grantResults.firstOrNull() == PackageManager.PERMISSION_GRANTED

      if(!audioRecordPermissionGranted){ // 요철 거절시 앱 종료
          finish()
      }
  }
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
  
#### Kotlin.class - Custom UI, MediaRecorder, MediaPlayer
+ MainActivity.kt
+ CountUpView
+ RecordButton
+ SoundVisualizerView
+ State
  

// 어렵댱ㅠㅠ


💡 data class, inner class, enum class 등 코틀린의 여러가지 클래스  
   (본 프로젝트에서 enum class를 어떻게 사용했는지)  
```KOTLIN
* State.kt

enum class State {
    BEFORE_RECORDING,
    ON_RECORDING,
    AFTER_RECORDING,
    ON_PLAYING
}

🥕 상태에 따라 버튼을 다르게 보여주기 위해 enum class를 사용
    BEFORE_RECORDING = 녹음전 > 빨간 동그라미버튼 (ic_record.xml) > 누르면 녹음을 시작한다는 시각적 효과를 위해
    ON_RECORDING = 녹음중 > 흰색 네모버튼 (ic_stop.xml) > 누르면 녹음을 그만둔다는 시각적 효과를 위해
    AFTER_RECORDING = 녹음후 > 흰색 삼각버튼 (ic_play.xml) > 누르면 녹음내용이 재생된다는 시각적 효과를 위해
    ON_PLAYING = 녹음재생중 > 흰색 네모버튼 (ic_stop.xml) > 누르면 녹음재생을 그만둔다는 시각적 효과를 위해
    
* RecordButton.kt
// 버튼을 상속받아서 커스터 마이징
// 뷰를 만들 때는 최소한 context와 attributeset 객체를 매개변수로 하는 생성자를 제공해야한다.

class RecordButton(
    context: Context,
    attrs: AttributeSet
): AppCompatImageButton(context, attrs) { 

    init {
        setBackgroundResource(R.drawable.shape_oval_button)
    }

    fun updateIconWithState(state: State){
        when(state){
            State.BEFORE_RECORDING ->{
                setImageResource(R.drawable.ic_record)
            }
            State.ON_RECORDING -> {
                setImageResource(R.drawable.ic_stop)
            }
            State.AFTER_RECORDING -> {
                setImageResource(R.drawable.ic_play)
            }
            State.ON_PLAYING -> {
                setImageResource(R.drawable.ic_stop)
            }
        }
    }
}

* MainActivity.kt 에서 사용

private var state = State.BEFORE_RECORDING
    set(value) { // setter 설정
        field = value // 실제 프로퍼티에 대입
        resetButton.isEnabled = (value == State.AFTER_RECORDING) ||
                (value == State.ON_PLAYING)
        recordButton.updateIconWithState(value)
    }
    
// set(value) {} 에서 field를 사용하는 이유에 대해서는 
// 코틀린에서 Getter와 Setter를 다루는 부분을 참고하여 공부하면 좋을듯함!
```
💡 attr ??  
```KOTLIN
* attr = attribute(속성, 옵션) 요정도의 의미로 해석하면 될듯함

custom view 만들 때 파라미터로 attr이 들어오며
보통은 value 폴더에 attrs.xml 파일을 생성하여 
여러 속성을 만들어 놓고, 그 속성들을 layout.xml 파일에 부여할 수 있음

이부분에 대해서 추가적인 공부 필요함!@!
```
💡 companion object [👉](https://www.bsidesoft.com/8187)  
   ```KOTLIN
   Java에서 static 사용하는 느낌?? 동작방식은 static 같이 보이지만 엄연한 차이가 존재하긴함
   
   이전 프로젝트인 timer 에서도 object객체생성에 대한 부분이 나왔던거 같은데
   확실하게 체크하기
   ```
💡 val vs const val  
```KOTLIN
* val은 런타임시 할당
* val로 선언한 변수는 코틀린에서 프로퍼티로 get() 함수를 가지는 변수이다.
  해당 변수를 직접 변경할 수 없지만 
  get() 함수의 처리 방식에 따라 의도한 값과 다른 값이 나올 수 있다. 즉, 항상 초깃값만 반환하는것은 아님!
  
  val str : String 
      get() { 
          return if (str.isEmpty()) { 
              "Jhdroid" 
          } else { 
              "Jhdroid_Blog" 
          }
      }
      
* const val은 컴파일시 할당
* const val로 선언한 변수는 코틀린에서 오직 문자열이나 기본 타입으로 할당돼야 함
  클래스나 함수 내부에서 선언 불가능(클래스의 프로퍼티나 지역 변수로 사용 불가능)
  변수를 최상위 레벨로 선언하거나 object로 선언한 클래스에서만 사용이 가능하다.
  
  object Constant { 
      const val num = 1234 
      const val str = "JhDroid" 
      
      const val main = MainActivity()  // 에러 발생
  }

즉, const는 함수나 어떤 클래스의 생성자에게도 결코 할당 될 수 없고 
오직 문자열이나 기본 자료형으로 할당되어야 한다.
const로 선언을 하면 클래스의 프로퍼티나 지역변수로 할당할 수 없기 때문에
일반적으로 companion object 안에 상수로 선언하게 된다.
(companion object 안에 const val로 선언한 변수는 자바에서 static final형)

// 컴파일 : 소스코드를 작성하고 컴파일 이라는 과정을 통해 기계어 코드로 변환되어 실행 가능한 프로그램이 됨
// 런타임 : 컴파일 과정을 마친 프로그램은 사용자에 의해 실행되어지며, 이러한 응용프로그램이 동작되어지는 때를 의미
```
💡 AppCompat ??
```KOTLIN
본 프로젝트 포함 이전 프로젝트에서도 Button대신 AppCompatButtom을 사용한 적이 있는데,
당시에는 그저 buttom 속성이 부여가 안돼서 AppCompat을 사용했다고 적었었는데
해당 내용에 대해 추가적으로 살펴보니 다음과 같은 답을 얻을수 있었다.

🥕 안드로이드는 매년 새 버전이 출시되고 있고, 이에 따라 구버전의 호환성을 제공해야 한다.
    AppCompat 클래스를 사용하면 기존 클래스를 래핑하여 이전 버전에서도 새 버전 출시된 것을
    정상적으로 동작하게 해준다.
```
