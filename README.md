```π‘ FastCampus κ°μ μκ° λ° μ λ¦¬```

### Voice_Recoder
+ Request runtime permissions(μνκΆν : λ§μ΄ν¬μ κ·Ό / λ§μ΄ν¬ κΆν λ°νμμ μ»κΈ°)  
  κΆμ₯λλ μμλ κ³΅μννμ΄μ§μ λμμμ(λ¬΄μ‘°κ±΄μ μΈκ±΄ μλ!)
+ external storage(μνκΆν : μ μ₯μ)
+ Custom View(Custom Drawing : μμ± μκ°ν canvas, onDraw)
+ MediaRecorder(λΉμ)
+ MediaPlayer(μ¬μ)

### Step
1. λΉμ μ  π 2. λΉμ μ€ π 3. λΉμ ν π 4. μ¬μ μ€  

κΈ°λ³Έμ μΈ μμλ μμ κ°μ΄ κ΅¬μ±νλ©°, [4.μ¬μ μ€]μΌ λ "μ μ§" λ²νΌμ λλ₯΄λ©΄ [3.λΉμ ν] λμκ° μ μλλ‘νκ³  "Reset" λ²νΌμ λλ₯΄λ©΄ [1.λΉμ μ ] μΌλ‘ λμκ° μ μλλ‘ νλ€.


<img src="https://user-images.githubusercontent.com/63087903/119835634-f76ca400-bf3b-11eb-85d3-461f27a1e588.jpg" width="200" height="430"> <img src="https://user-images.githubusercontent.com/63087903/119835628-f63b7700-bf3b-11eb-8a89-12073bdc68cc.jpg" width="200" height="430">

### [2021-05-12]
### [2021-07-23 ing~~]

### manifest
+ μ€λμ€ λΉμκΈ°λ₯κ³Ό, μΈλΆ μ μ₯μ μ κ·Ό κΆν μΆκ°
  ```KOTLIN
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
  ```
+ MainActivity.kt
  ```KOTLIN
  * μμ²­ν  κΆνλ€μ λ΄μ λ°°μ΄μ μμ± λΉμ κ΄λ ¨ κΆνμ λ΄μμ€λ€.
    (μ΄λ κ² νλ μ΄μ λ λ³΄ν΅ κ·λͺ¨κ° μλ μ±μμλ λ¨μΌκΆνμ΄ μλλΌ μ¬λ¬ κΆνμ λ°μμ€κΈ° λλ¬Έμ λ°°μ΄μ λ΄λλ€... 
    κ³  μκ°νμλλ° μ μ΄μ requestPermissions λ©μλκ° λ°λ νλΌλ―Έν°κ° λ°°μ΄κ°μ) 
    
  private val requiredPermissions = arrayOf(
      android.Manifest.permission.RECORD_AUDIO,
      android.Manifest.permission.READ_EXTERNAL_STORAGE
  )
    
  * onCreate() μμ requestAudioPermission() ν¨μλ₯Ό νΈμΆνκ³  ν¨μ λ΄λΆμμ
    requestPermissions λ©μλ νΈμΆ(νλΌλ―Έν°λ‘ κΆνμ λ΄μ λ°°μ΄κ³Ό, λ¦¬νμ€νΈ μ½λλ²νΈκ° μ£Όμ΄μ§)
    κΆν μμ²­μ λ°λ₯Έ μ¬μ©μμ λ΅λ³μ onRequestPermissionsResultλ₯Ό μ¬μ μ ν¨μΌλ‘μ μ²λ¦¬νλ€.
  
  private fun requestAudioPermission(){
      requestPermissions(requiredPermissions, REQUEST_RECORD_AUDIO_PERMISSION)
  } 
  
  // REQUEST_RECORD_AUDIO_PERMISSION λ companion objectλ‘ μ μΈν μμκ° 201 μ΄λ€.

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

      if(!audioRecordPermissionGranted){ // μμ²  κ±°μ μ μ± μ’λ£
          finish()
      }
  }
  ```

### layout.xml
+ activity_main μ Custom UIλ₯Ό κ·Έλ¦¬κΈ° μν View Class λ§λ€κΈ° [π](https://developer.android.com/training/custom-views/create-view?hl=ko)
  ```KOTLIN
  // activity_main.xml
    
  <com.com.voicerecoder.SoundVisualizerView ... />
  <com.com.voicerecoder.CountUpView ... />
  <com.com.voicerecoder.RecordButton ... />

  // kotlin.kt
  
  SoundVisualizerView.kt
  CountUpView.kt
  RecordButton.kt
  
  * κ° λ·°μν΄λΉνλ ν΄λμ€ νμΌλ€μ μμ±
  ```
+ Custom Drawing [π](https://developer.android.com/training/custom-views/custom-drawing?hl=ko)  
  record λ‘ μ μ₯ν λΉμ νμΌ > μ΄λ―Έμ§ μκ°ν νλ λΆλΆ : Visualizer
  ```KOTLIN
  * SoundVisualizerView.kt
  ```
  
### Kotlin.class - Custom UI, MediaRecorder, MediaPlayer
+ MainActivity.kt
+ CountUpView
+ RecordButton
+ SoundVisualizerView
+ State
  

// μ΄λ ΅λ±γ γ 


#### π‘ data class, inner class, enum class λ± μ½νλ¦°μ μ¬λ¬κ°μ§ ν΄λμ€  
+ (λ³Έ νλ‘μ νΈμμ enum classλ₯Ό μ΄λ»κ² μ¬μ©νλμ§)  
```KOTLIN
* State.kt

enum class State {
    BEFORE_RECORDING,
    ON_RECORDING,
    AFTER_RECORDING,
    ON_PLAYING
}

π₯ μνμ λ°λΌ λ²νΌμ λ€λ₯΄κ² λ³΄μ¬μ£ΌκΈ° μν΄ enum classλ₯Ό μ¬μ©
    BEFORE_RECORDING = λΉμμ  > λΉ¨κ° λκ·ΈλΌλ―Έλ²νΌ (ic_record.xml) > λλ₯΄λ©΄ λΉμμ μμνλ€λ μκ°μ  ν¨κ³Όλ₯Ό μν΄
    ON_RECORDING = λΉμμ€ > ν°μ λ€λͺ¨λ²νΌ (ic_stop.xml) > λλ₯΄λ©΄ λΉμμ κ·Έλ§λλ€λ μκ°μ  ν¨κ³Όλ₯Ό μν΄
    AFTER_RECORDING = λΉμν > ν°μ μΌκ°λ²νΌ (ic_play.xml) > λλ₯΄λ©΄ λΉμλ΄μ©μ΄ μ¬μλλ€λ μκ°μ  ν¨κ³Όλ₯Ό μν΄
    ON_PLAYING = λΉμμ¬μμ€ > ν°μ λ€λͺ¨λ²νΌ (ic_stop.xml) > λλ₯΄λ©΄ λΉμμ¬μμ κ·Έλ§λλ€λ μκ°μ  ν¨κ³Όλ₯Ό μν΄
    
* RecordButton.kt
// λ²νΌμ μμλ°μμ μ»€μ€ν° λ§μ΄μ§
// λ·°λ₯Ό λ§λ€ λλ μ΅μν contextμ attributeset κ°μ²΄λ₯Ό λ§€κ°λ³μλ‘ νλ μμ±μλ₯Ό μ κ³΅ν΄μΌνλ€.

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

* MainActivity.kt μμ μ¬μ©

private var state = State.BEFORE_RECORDING
    set(value) { // setter μ€μ 
        field = value // μ€μ  νλ‘νΌν°μ λμ
        resetButton.isEnabled = (value == State.AFTER_RECORDING) ||
                (value == State.ON_PLAYING)
        recordButton.updateIconWithState(value)
    }
    
// set(value) {} μμ fieldλ₯Ό μ¬μ©νλ μ΄μ μ λν΄μλ 
// μ½νλ¦°μμ Getterμ Setterλ₯Ό λ€λ£¨λ λΆλΆμ μ°Έκ³ νμ¬ κ³΅λΆνλ©΄ μ’μλ―ν¨!
```
#### π‘ attr ??  
```KOTLIN
* attr = attribute(μμ±, μ΅μ) μμ λμ μλ―Έλ‘ ν΄μνλ©΄ λ λ―ν¨

custom view λ§λ€ λ νλΌλ―Έν°λ‘ attrμ΄ λ€μ΄μ€λ©°
λ³΄ν΅μ value ν΄λμ attrs.xml νμΌμ μμ±νμ¬ 
μ¬λ¬ μμ±μ λ§λ€μ΄ λκ³ , κ·Έ μμ±λ€μ layout.xml νμΌμ λΆμ¬ν  μ μμ

μ΄λΆλΆμ λν΄μ μΆκ°μ μΈ κ³΅λΆ νμν¨!@!
```
#### π‘ companion object [μ°Έμ‘°π](https://www.bsidesoft.com/8187)  
   ```KOTLIN
   Javaμμ static μ¬μ©νλ λλ?? λμλ°©μμ static κ°μ΄ λ³΄μ΄μ§λ§ μμ°ν μ°¨μ΄κ° μ‘΄μ¬νκΈ΄ν¨
   
   μ΄μ  νλ‘μ νΈμΈ timer μμλ objectκ°μ²΄μμ±μ λν λΆλΆμ΄ λμλκ±° κ°μλ°
   νμ€νκ² μ²΄ν¬νκΈ°
   ```
#### π‘ val vs const val  
```KOTLIN
* valμ λ°νμμ ν λΉ
* valλ‘ μ μΈν λ³μλ μ½νλ¦°μμ νλ‘νΌν°λ‘ get() ν¨μλ₯Ό κ°μ§λ λ³μμ΄λ€.
  ν΄λΉ λ³μλ₯Ό μ§μ  λ³κ²½ν  μ μμ§λ§ 
  get() ν¨μμ μ²λ¦¬ λ°©μμ λ°λΌ μλν κ°κ³Ό λ€λ₯Έ κ°μ΄ λμ¬ μ μλ€. μ¦, ν­μ μ΄κΉκ°λ§ λ°ννλκ²μ μλ!
  
  val str : String 
      get() { 
          return if (str.isEmpty()) { 
              "Jhdroid" 
          } else { 
              "Jhdroid_Blog" 
          }
      }
      
* const valμ μ»΄νμΌμ ν λΉ
* const valλ‘ μ μΈν λ³μλ μ½νλ¦°μμ μ€μ§ λ¬Έμμ΄μ΄λ κΈ°λ³Έ νμμΌλ‘ ν λΉλΌμΌ ν¨
  ν΄λμ€λ ν¨μ λ΄λΆμμ μ μΈ λΆκ°λ₯(ν΄λμ€μ νλ‘νΌν°λ μ§μ­ λ³μλ‘ μ¬μ© λΆκ°λ₯)
  λ³μλ₯Ό μ΅μμ λ λ²¨λ‘ μ μΈνκ±°λ objectλ‘ μ μΈν ν΄λμ€μμλ§ μ¬μ©μ΄ κ°λ₯νλ€.
  
  object Constant { 
      const val num = 1234 
      const val str = "JhDroid" 
      
      const val main = MainActivity()  // μλ¬ λ°μ
  }

μ¦, constλ ν¨μλ μ΄λ€ ν΄λμ€μ μμ±μμκ²λ κ²°μ½ ν λΉ λ  μ μκ³  
μ€μ§ λ¬Έμμ΄μ΄λ κΈ°λ³Έ μλ£νμΌλ‘ ν λΉλμ΄μΌ νλ€.
constλ‘ μ μΈμ νλ©΄ ν΄λμ€μ νλ‘νΌν°λ μ§μ­λ³μλ‘ ν λΉν  μ μκΈ° λλ¬Έμ
μΌλ°μ μΌλ‘ companion object μμ μμλ‘ μ μΈνκ² λλ€.
(companion object μμ const valλ‘ μ μΈν λ³μλ μλ°μμ static finalν)

// μ»΄νμΌ : μμ€μ½λλ₯Ό μμ±νκ³  μ»΄νμΌ μ΄λΌλ κ³Όμ μ ν΅ν΄ κΈ°κ³μ΄ μ½λλ‘ λ³νλμ΄ μ€ν κ°λ₯ν νλ‘κ·Έλ¨μ΄ λ¨
// λ°νμ : μ»΄νμΌ κ³Όμ μ λ§μΉ νλ‘κ·Έλ¨μ μ¬μ©μμ μν΄ μ€νλμ΄μ§λ©°, μ΄λ¬ν μμ©νλ‘κ·Έλ¨μ΄ λμλμ΄μ§λ λλ₯Ό μλ―Έ
```
#### π‘ AppCompat ??
```KOTLIN
λ³Έ νλ‘μ νΈ ν¬ν¨ μ΄μ  νλ‘μ νΈμμλ Buttonλμ  AppCompatButtomμ μ¬μ©ν μ μ΄ μλλ°,
λΉμμλ κ·Έμ  buttom μμ±μ΄ λΆμ¬κ° μλΌμ AppCompatμ μ¬μ©νλ€κ³  μ μμλλ°
ν΄λΉ λ΄μ©μ λν΄ μΆκ°μ μΌλ‘ μ΄ν΄λ³΄λ λ€μκ³Ό κ°μ λ΅μ μ»μμ μμλ€.

π₯ μλλ‘μ΄λλ λ§€λ μ λ²μ μ΄ μΆμλκ³  μκ³ , μ΄μ λ°λΌ κ΅¬λ²μ μ νΈνμ±μ μ κ³΅ν΄μΌ νλ€.
    AppCompat ν΄λμ€λ₯Ό μ¬μ©νλ©΄ κΈ°μ‘΄ ν΄λμ€λ₯Ό λννμ¬ μ΄μ  λ²μ μμλ μ λ²μ  μΆμλ κ²μ
    μ μμ μΌλ‘ λμνκ² ν΄μ€λ€.
```
