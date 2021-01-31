---
layout: post
title: boostcourse_kotilin
published: false
---



# 변수와 자료형, 연산자

## 1. 변수

### 자료형
- Int 정수 1, 2, 3
- String 문자열 "Hello123" 일종의 배열 특수한 자료형
- Float 실수 1.2 

### 변수
- val (value) - 불변형 (immutable)
- var (variable) - 가변형 (mutable)


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

### 변수 선언의 예
- val username = "Kildong"  -> 자료형을 추론하여 String으로 결정
- var username: -> 자료형을 지정하지 않은 변수는 사용할 수 없다
- val init: Int -> 사용 전 혹은 생성자 시점에서 init변수를 초기화 해야함
- val number = 10 ->  number 변수는 Int형으로 추론


###  cf) 변수명은 예약어 x 숫자시작 x 이왕이면 카멜 표기법으로!

### 카멜 표기법
1. 일반 변수, 함수명 -> 소문자 시작 첫 단어는 대문자 ex) camelCase
2. 클래스, 인터페이스 -> 대문자 시작 첫 단어는 대문자 ex) AnimalCategory


<br/><br/>


## 2. 자료형

### 기본형
- 가공되지 않은 순수한 자료형으로 프로그래밍 언어에 내장
- int, long, float, double


### 참조형
- 동적 공간에 데이터를 둔 다음 이것을 참조하는 자료형
- ex) Int, Long, Float, Double 등



### cf) 코틀린에서는 참조형을 통해서만 데이터를 다룬다

### 기본형은 메모리에 값이 참조형은 메모리에 주소가 들어간다

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


<br/>
<br/><br/>
<br/>


## Null을 허용한 변수 검사

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






## 3. 코틀린 프로그래밍 응용 안드로이드 편

- 안드로이드의 앱 실무
- 안드로이드의 기본 요소
- 프로젝트 실무 
- 다양한 서드파티 라이브러리 
- 디버깅 기법 
- 저장소 관리 
- 앱 배포 등등


# 강사님 소개


강의 진행 : 황영덕 
안드로이드 포팅 관련 업무
안드로이드 관련 교육 진행
코틀린을 이용해서 어떻게 빠르게 앱을 만들것인가 
멀티플랫폼 앱을위해서 연구
현재 호주에서 일하고 있고 플러터를 이용중
개발자 역량 -> 호기심이 강해야함 
논리적인 사고와 분석 능력
무엇보다도 문제를 해결하기 위해 빠르게 검색하고 빠르게 적용할 수 있는 오픈 마인드가 중요하다
반복적인 일이 많다면 이를 줄이기 위한 생각과 프로세스를 간략하게 할 수 있도록 추진력과 모험심

코틀린 : 문법을 익히는 것부터 시작 실무적인 여러 사례를 통해 문법을 적용해보면서 배우기 자바를 어느정도 이해하고 있다면 많은 도움이 됨

수강생에게 한마디!
노력해서 만든 것 재미있게 했으면 좋겠다!


------------------------------------------------

------------------코틀린이란 무엇일까?-----------



# 코틀린 너는 누구니

## 컴퓨터 언어
1. 어셈블리 언어 최하위 언어 사람이 이해하기 어려움
2. 절차지향형 언어 c언어 하드웨어를 다루는데 인간친화적
3. 객체지향형 언어 자바  대형 소프트웨어 만드는데 적합, 스마트폰에서도 앱들이 자방 가상 머신에서도 도록 있다
4. 애플 : 오브젝트C에서 스위프트로 넘어감
5. 구글 : 자바에서 코틀린으로 


## 코틀린 탄생 배경 

1. 목표 : 풀스택 웹 개발, 안드로이드, IOS, 임베디드 IOT 등 모든 개발을 다양한 플랫폼에서 개발할 수 있도록 하는 것

2. 특징 
- IDE로 유명한 JetBrains에서 개발하고 보급
- 간결한 코드, 세미클론 옵션
- 변수는 Nullable과 NotNull로 나뉘는데 변수 선언시 '?'를 붙여 Nullable로 만들 수 있다.


## 코틀린 사용 가능한 플랫폼

- kotlin/jvm - 자바 가상 머신 <<여기 집중!>>
- kotlin/JS - 자바스크립트에 의해 브라우저에서 동작하는 앱을 만들 수 있다. (웹)
- kotlin/Native - LLVM 기반의 네이티브 컴파일을 지원해 여러 타깃의 앱을 만들 수 있다. 

cf ) kotlin/naive에서의 타깃
IOS(arm64, emulator), MacOS, Android(arm64), Windows(X86), Linux, WebAssembly(wasm32)


## 코틀린의 장점

- 자료형에 대한 오류를 미리 잡을 수 있는 정적 언어(Statically typed) 정적 형식 : 컴파일러가 타입을 검증해 준다.
- 널 포인터로 인한 프로그램의 중단을 예방할 수 있다.
보통 개발자들은 코틀린의 이런 특징을 'NPE에서 자유롭다'라고 한다.
- 데이터형 선언 시 널 가능한 형식과 불가능한 형식 지원
- 자바와 완벽하게 상호운영이 가능하다.
- 아주 간결하고 효율적
- 함수형 프로그래밍과 객체 지향 프로그래밍이 모두 가능
- 세미콜론 생략할수 있다.


-----------------------------------------------------------------



-------------개발 환경을 꾸며 보아요--------

## JDK

Oracle JDK vs OpenJDK
Oracle JDK : 보안 업데이트를 지속적으로 제공
OpenJDK : 제한 없이 사용 가능, 보안 서비스의 의무는 X


## Azul의 Julu
- TCK 인증을 통과한 OpenJDK를 묶어서 베포하는 제 3의 벤더


## JDK -> 이미 설치되어 있어서 기존 것으로 대체


## Helloworld 찍기

```java
fun main() {
    println("HelloKotlin!")
}
```

### 결과물


<img src="https://i.imgur.com/yWFUoo8.png" width=500>




-----------------------------------------------------------------------


------------안녕 세상아 ---------------


## 인텔리제이 설정 관련

파일 -> settings 

- 폰트 변경 : font 검색후 Editor에서 Font 변경


## main 함수
main -> 진입 점
<br/><br/>

### 실행
Alt shift F10 (최초에 config가 없을 때)
shfit F10 (이미 config가 있을 때)
<br/><br/>

## 인자가 없는 main

```java
fun main() {
    println("HelloKotlin!")
    println("Hello!")
}
```


- fun은 function의 약자
- println : 콘솔 창에 출력할 때 씀



### cf) ctrl b : 사용한 함수의 라이브러리 확인 가능 



## 인자가 있는 main

run config로 가서 argument에 넣어줘야 한다.


<img src="https://i.imgur.com/cVjGFTg.png" width=800>




```java
fun main(args: Array<String>) {
    println("args[0] = ${args[0]}")
    println(args[1])
    println(args[2])
    println(args[3])
}
```



## 동작 방식

kt -> java코드 -> jvm에서 실행 



<img src="https://i.imgur.com/F3Nf8eJ.png" width=800>





### class가 없는데 main 메서드 하나로 println을 콘솔에서 실행하고 있다. 실제로는 main 매서드는 파일명을 기준으로 자동으로 클래스가 생성된다 이를 확인하기 위해 

### Tools에 Kotlin이라는 메뉴에 show byte code 클릭하면 어떻게 실행됐는지 확인 하는 것 decompile을 누르면 익숙한 자바 코드가 보인다








## -> 코틀린은 자바에 비해 훨씬 간결한 것을 알 수 있다



# 단축키

Messages Alt + 0 (Cmd + 0)
Project Alt + 1 (Cmd + 1)
Favorites Alt + 2 (Cmd + 2)
Run Alt + 4 (Cmd + 4)
Debug Alt + 5 (Cmd + 5)
TODO              Alt + 6 (Cmd + 6)
Structure Alt + 7 (Cmd + 7)
Terminal Alt + F12 (Option + F12)
줄 복사 : ctrl + D








