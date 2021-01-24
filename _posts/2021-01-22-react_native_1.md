---
title: "react_native 맛보기 1"
categories: react_native react app
date: 2021-01-22
last_modified_at: 2021-01-22
---


<br/><br/><br/>


## 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 환경 설정하기

<br/>
<br/>

> [환경 설정 참고 블로그](https://dev-yakuza.posstree.com/ko/react-native/install-on-windows/);


# 마지막 확인 부분에서
<br/><br/>

## 1. andorid 폴더 아래에 local.properites 추가
<br/>
환경 변수 설정을 하나 안 해줘서 문제가 생긴 것 같은데 일단은 local.properties 파일을 추가해서 

```java
sdk.dir=C\:\\Users\\triplej\\AppData\\Local\\Android\\Sdk 

```

를 적어준다 

<br/><br/><br/>


## 2. sdk 설치 문제


<br/>
가르쳐줬던 sdk를 설치했음에도 불구하고 

```java

Could not determine the dependencies of task ':app:installDebug'.
> Failed to install the following Android SDK packages as some licences have not been accepted.
     platforms;android-29 Android SDK Platform 29
  To build this project, accept the SDK license agreements and install the missing components using the Android Studio SDK Manager.
```

라는 오류가 나서 안드로이드 스튜디오에 다시 가서 sdk 29 설치를 완료해줬다




<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/xejLqNH.png" width=500>



