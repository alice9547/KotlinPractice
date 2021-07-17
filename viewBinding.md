# viewBinding

1. findViewById -> 보통 자바에서 사용

2. Kotlin Extension -> 정말 편하기는 함 -> 다만 자바에서는 사용 불가 + 일부 오류가 발생할 확률 존재

3. 바인딩 사용

=============================

뷰와 코드를 연결하는 방법 _ viewBinding

1)  build.gradle에 viewBinding 설정 추가

```kotlin
android {
/////////////////////////////
    buildFeatures {
        viewBinding true
    }
///////////////////////////////////추가
    compileSdkVersion 30
    buildToolsVersion "30.0.3"
```

2) Sync Now 로 설정 적용

3) 레이아웃 파일 바인딩으로 생성

ex) 파일이름 변경                              activity_main.xml                 ->             ActivityMainBinding

```kotlin
val binding = ActivityMainBinding.inflate(layoutInflater)
setContentView(binding.root)
```

4) id에 리스너 설정(내부 코드 동작)

```kotlin
setContentView(binding.root)
binding.btnSay.setOnClickListener {      //동작할 코드
            binding.textSay.text = "Hello Kotlin!!"
        }
```

5) 전체 코드

```kotlin
package com.example.kotlin

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import com.example.kotlin.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val binding = ActivityMainBinding.inflate(layoutInflater)

        setContentView(binding.root)
        binding.btnSay.setOnClickListener {
            binding.textSay.text = "Hello Kotlin!!"
        }
    }
}
```
