---
title: "부스트코스 코틀린 2"
categories: boostcourse kotlin
date: 2021-02-04
last_modified_at: 2021-02-04
---


<br/><br/>


# 변수와 자료형, 연산자


<br/><br/><br/>

## 1. 변수

<br/>

### 자료형
- Int 정수 1, 2, 3
- String 문자열 "Hello123" 일종의 배열 특수한 자료형
- Float 실수 1.2 

<br/>

### 변수
- val (value) - 불변형 (immutable)
- var (variable) - 가변형 (mutable)

<br/>

### ex ) val username: String = "Kildong"

```java

fun main(){

    val username: String = "Kildong"
    // username = "Dooly" 불변형이라 바꿀 수 없음

    var username2: String = "Kildong"
    username2 = "dooly" //var이라 가능



    println("username : ${username}")
    println("username : ${username2}")


    // 이런식으로 추론형으로 쓸 수도 있다
    // ctrl + shift + p 로 확인 가능
    var username3 = "kildong"
    var count = 3;

    println("username: $username, count $count")



}
```

<br/>


### 변수 선언의 예
- val username = "Kildong"  -> 자료형을 추론하여 String으로 결정
- var username: -> 자료형을 지정하지 않은 변수는 사용할 수 없다
- val init: Int -> 사용 전 혹은 생성자 시점에서 init변수를 초기화 해야함
- val number = 10 ->  number 변수는 Int형으로 추론

<br/>


###  cf) 변수명은 예약어 x 숫자시작 x 이왕이면 카멜 표기법으로!


<br/>

### 카멜 표기법
1. 일반 변수, 함수명 -> 소문자 시작 첫 단어는 대문자 ex) camelCase
2. 클래스, 인터페이스 -> 대문자 시작 첫 단어는 대문자 ex) AnimalCategory


<br/><br/>


## 2. 자료형

### 기본형
- 가공되지 않은 순수한 자료형으로 프로그래밍 언어에 내장
- int, long, float, double

<br/>


### 참조형
- 동적 공간에 데이터를 둔 다음 이것을 참조하는 자료형
- ex) Int, Long, Float, Double 등

<br/>


### cf) 코틀린에서는 참조형을 통해서만 데이터를 다룬다

<br/>

### 기본형은 메모리에 값이 참조형은 메모리에 주소가 들어간다

<br/>
<br/>

### 1. 정수형 
- Long 8바이트
- Int 4바이트
- Short 2바이트
- Byte 1바이트
- 부호가 없는 것은 U를 붙여서 양수만 표현 (두배로 가능)
- 기본으로는 Int로 추론 됨, 값이 커지면 Long으로 추론
- 접미사 접두사를 사용하면 ex) 0x->16진 표기가 된 Int 123L-> Long형
- 명시적으로 자료형을 지정해도 됨
- 큰 수를 읽기 쉽게 하는 방법 : val number = 1_000_000 언더바 넣기

<br/>

### 2. 실수형
- Double 8바이트
- Float 4바이트
- 마지막에 F를 붙이면 Float 아니면 double형이 기본

### Cf) 부동소수점
[ 부동 소수점 참고 블로그 ](https://www.secmem.org/blog/2020/05/15/float/)


<br/><br/>


```java

fun main() {
    var num: Double = 0.1

    for(x in 0..999){

        num += 0.1
    }

    println("num: $num")


    // 100이 나와야 되는데
    // num: 100.09999999999859
    // 뒤에 이상한 숫자가 붙는다 -> 공간 제약에 따른 부동 소수점 연산의 단점
}
```
<br/><br/>

### cf) 각 자료형 별 최소 최대

```java


fun main() {
    println("Int: ${Int.MIN_VALUE}~${Int.MAX_VALUE}")
    println("Byte: ${Byte.MIN_VALUE}~${Byte.MAX_VALUE}")
    println("Short: ${Short.MIN_VALUE}~${Short.MAX_VALUE}")
    println("Long: ${Long.MIN_VALUE}~${Long.MAX_VALUE}")
    println("Float: ${Float.MIN_VALUE}~${Float.MAX_VALUE}")
    println("Double: ${Double.MIN_VALUE}~${Double.MAX_VALUE}")

    //Int: -2147483648~2147483647
    //Byte: -128~127
    //Short: -32768~32767
    //Long: -9223372036854775808~9223372036854775807
    //Float: 1.4E-45~3.4028235E38
    //Double: 4.9E-324~1.7976931348623157E308

}
```

<br/>

### cf) 2의 보수 
- 음수는 2의 보수 표현을 사용해 연산됨
- 절대값의 이진수에 값을 뒤집고 1을 더함


<br/>
<br/>

### 3. 논리형
- Boolean 1비트 true or false
- ex) val isUploaded: Boolean

<br/><br/>

### 4. 문자형
- Char 2바이트 


<br/><br/>


### 5. 문자열 (String)
- String으로 선언되며 배열로 처리된다
- 값을 변경하면 새로운 공간에 만들어진다
- ==는 값만 비교 ===는 참조까지 비교

```java


fun main() {
    var str1: String = "Hello"
    var str2 = "World"
    var str3 = "Hello"

    println("str1 === str2 ${str1 === str2}")
    println("str1 === str3 ${str1 === str3}") //변수 이름만 다르고 같은 공간을 가르키고 있기 때문에 true
}



```


<br/>
<br/>

### cf) 표현식에서 문자열

```java


fun main() {
    var a = 1
    val str1 = "a = $a"
    val str2 = "a = ${a+2}" //문자열에 표현식 사용

    println("str1: \"$str1\", str2: \"$str2\"")


    //str1: "a = 1", str2: "a = 3"

}
```


<br/><br/>


