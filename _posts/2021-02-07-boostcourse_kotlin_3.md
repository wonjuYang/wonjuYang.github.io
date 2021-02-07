---
title: "부스트코스 코틀린 3"
categories: boostcourse kotlin
date: 2021-02-07
last_modified_at: 2021-02-07
---


<br/><br/>


## 2. Null을 허용한 변수 검사


<br/>
<br/>


- 코틀린의 변수 선언은 기본적으로 null을 허용하지 않는다
- val a: Int, var b: String -> X 꼭 초기화 해줘야함
- val a: Int? = null, var b: String? = null -> O 가능함
- NPE(NullPointerException) : 사용할 수 없는 null인 변수에 접근하면서 발생하는 예외


```java


fun main() {

    var str1: String
    //str1 = null // 기본형은 null을 허용하지 않는다
    // println(str1) <<오류 반드시 initialize 해야한다

    var str2: String?
    str2 = null
    //println("str2: $str2, length: ${str2.length}) <<Null일 가능성이 있기때문에 점 찍고 접근할수 없다
    println("str2: $str2, length: ${str2?.length}") // null을 확인하는 ?를 삽입 -> safecall
    // println("str2: $str2, length: ${str2!!.length}") // null일리가 없다 !! null이면 문제가 발생한다

    // var len = if (str2 != null) str2.length else -1

    //위의 식을 elvis expression으로 바꾸면 이렇게 된다
    // length가 null이 아니면 length 들어가고 null이면 -1 
    var len = str2?.length ?: -1

    println("str2: $str2, length: $len")


}
```

<br/>
<br/>


### 정리
- Kotlin에서는 기본적으로 NotNull이고 Nullable 표현에만 '?'가 사용된다
- 세이프 콜 str1?.length
- non-null 단정 기호 str1!!.length 사용하지 않는 것이 낫다
- elvis 연산자를 이용하면 더 짧게 표현 가능

<br/>
<br/>
<br/>
<br/>



<br/><br/>


