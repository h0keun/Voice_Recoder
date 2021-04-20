### Voice_Recoder

+ Request runtime permissions(위험권한 : 마이크접근)  
  권장되는 순서는 공식홈페이지에 나와있음(무조건적인건 아님!)
+ external storage
+ Custom View(음성 시각화)
+ MediaRecorder(음성 녹음)

### check list
+ enum class
+ companion object
+ set(value) {  
  field = value  
  ...  
  }


### Step
1. 녹음 전 👉 2. 녹음 중 👉 3. 녹음 후 👉 4. 재생 중  

기본적인 순서는 위와 같이 구성하며, [4.재생 중]일 때 "정지" 버튼을 누르면 [3.녹음 후] 돌아갈 수 있도록하고 "Reset" 버튼을 누르면 [1.녹음 전] 으로 돌아갈 수 있도록 한다.
