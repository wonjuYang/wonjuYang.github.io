---
title: "부스트코스 코틀린 1"
categories: boostcourse kotlin
date: 2021-01-30
last_modified_at: 2021-01-30
---

<br/><br/><br/>
--------------오리엔테이션-----------------

# 강의 커리큘럼 설명

## 1. 코틀린 프로그래밍 기본 - 함수형편

### 코틀린이란 ?
- 구글에서 지정한 안드로이드 공식 언어
- 자바와 100% 호환성! 라이브러리를 그대로
- 기본적으로 JVM상에서 동작 시키지만 다양한 플랫폼에서도 실행 가능
- 함수형 프로그래밍 기법인 람다식, 고차함수를 제공하면서 코드의 축약 및 최적화 가능
- 객체지향 프로그래밍 기법도 같이 제공하는 멀티 패러다임 언어!
- 생산성이 매우 높은 언어!


## 2. 코틀린 프로그래밍 기본 - 객체지향 편

- 클래스, 객체, 인터페이스 
- 제네릭
- 배열과 컬렉션
- 다양한 클래스 기법


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


<br/><br/><br/>

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

<br/><br/><br/>


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




<br/><br/><br/>


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





### class가 없는데 main 메서드 하나로 println을 콘솔에서 실행하고 있다.
### 실제로는 main 매서드는 파일명을 기준으로 자동으로 클래스가 생성된다 
### 이를 확인하기 위해 Tools에 Kotlin이라는 메뉴에 show byte code 클릭하면 어떻게 실행됐는지 확인 하는 것 decompile을 누르면 익숙한 자바 코드가 보인다





<br/><br/>


## -> 코틀린은 자바에 비해 훨씬 간결한 것을 알 수 있다

<br/><br/><br/><br/><br/>

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








