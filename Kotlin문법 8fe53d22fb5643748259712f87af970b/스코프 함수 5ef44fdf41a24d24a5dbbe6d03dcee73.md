# 스코프 함수

→ 코드를 축약해서 표현할 수 있도록 도와주는 함수. (= 영역 함수)

## run & let

→ 자신의 스코프 안에서 호출한 대상을 this와 it으로 대체해서 사용 가능

### run

→ 스코프 함수 안에서 호출한 대상을 this로 사용.

→ this를 생략하고 메서드나 프로퍼티를 바로 사용 가능

```kotlin
var list = mutableListOf("Scope", "Function")
        list.run {
            val listSize = size    //this.size 의 this. 생략
            println("리스트 길이 run = $listSize")
        }
```

### let

→ 스코프 안에서 호출한 대상을 it으로 사용 가능

→ it은 생략 불가능, target 등 다른 이름으로 바꾸기 가능

```kotlin
var list = mutableListOf("Scope", "Function")
        list.let {
            val listSize = it.size  //모든 속성과 함수를 it.멤버로 사용가능
            println("리스트 길이 let = $listSize")
        }
```

## this와 it으로 구분

### this 사용 스코프 함수 : run, apply, with

```kotlin
var list = mutableListOf("Scope", "Function")
        
list.apply {
    val listSize = size  //모든 속성과 함수를 it.멤버로 사용가능
    println("리스트 길이 apply = $listSize")
}

with (list) {
    val listSize = size  //모든 속성과 함수를 it.멤버로 사용가능
    println("리스트 길이 with = $listSize")
}
```

→ 호출 대상이 null일 경우는 apply, run으로 사용 → with은 확장 함수가 아니기에.

### it 사용 스코프 함수 : let, also

```kotlin
var list = mutableListOf("Scope", "Function")

list.let { target ->
    val listSize = target.size  //모든 속성과 함수를 it.멤버로 사용가능
    println("리스트 길이 let = $listSize")
}

list.also { 
    val listSize = it.size  //모든 속성과 함수를 it.멤버로 사용가능
    println("리스트 길이 also = $listSize")
}
```

## 반환값으로 구분

→ 결과값을 반활할 경우, 스코프가 종료되는 시점에서의 반환값이 다르기에 다른 역할의 함수 필요

### this 자체를 반환하는 스코프 함수 : apply, also

→ 스코프 함수 안에서 코드 완료되면 뒷 코드가 뭐가 있든 자기 자신을 리턴한다.

### 마지막 실행 코드 반환하는 스코프 함수 : let, run, with

→ 무조건 자기 자신이 아니라 마지막 실행 코드를 리턴한다.