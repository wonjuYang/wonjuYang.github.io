---
title: "부스트코스 코틀린 4"
categories: boostcourse kotlin
date: 2021-02-10
last_modified_at: 2021-02-10
---



## 3. 자료형 비교, 검사, 변환


<br/>


### 1. 코틀린 자료형 변환

<br/>

- 기본형을 사용하지 않고 참조형만 ㅅ용
- 서로 다른 자료형은 변환 과정을 거친 후 비교
- 변환 메소드 사용 

```java

val a: Int = 1
val b: Double = a.toDouble
val result = 1L + 3 //Long +Int -> result는 Log

```

- to + 자료형 하면 변환 가능

<br/>

- 이중 등호 : 값만 비교하는 경우
- 삼중 등호 : 값과 참조 주소를 비교할 때

- cf) 참조 주소가 달라지는 경우

```java
val a: Int = 128 //기본형
val b: Int? = 128 //객체 (동적공간)

println(a==b) //true
println(a===b) //false




```

<br/>


```java

fun main() {
    val a: Int = 128
    // val b: Double = a //에러
    val b:Double = a.toDouble() //정상 작동

    val c: Int? = a
    val d: Int? = a
    val e: Int? = c

    println(c == d) //true
    println(c === d) //false ? 를 붙여서 새롭게 주소를 만들었음
    println(c === e) //true c의 주소값이 저장되어있음
}

```


<br/>
<br/>


### cf) 스마트 캐스트

- 구체적으로 명시되지 않은 자료형을 자동 변환
- 값에 따라 자료형을 결정
- Number형은 숫자를 저장하기 위한 특수한 자료형으로 스마트 캐스팅 됨


<br/>
<br/>
<br/>



### 2. 자료형 검사
- is 키워드를 사용한 검사

```java

val num = 256

if(num is Int){
    println(num)
}else if(num !is Int){
    print("not int")
}

```


<br/>
<br/>
<br/>

### 3. Any
- 자료형이 정해지지 않은 경우
- 모든 클래스의 뿌리 - Int나 String은 Any형의 자식 클래스
- Any는 언제든 필요한 자료형으로 자동 변환


```java

var a: Any = 1
a = 20L //Long이 됨
println("a: $a type: ${a.javaClass}") //a형의 자바 기본형 출력하면 long이 나옴


```


- any를 활용한 함수

```java


fun main() {
    checkArg("Hello")
    checkArg(5)
}

fun checkArg(x: Any){

    if(x is String){
        println("X is String: $x")
    }

    if( x is Int ){
        println("x is Int: $x" )
    }
}

```

<br/><br/>


