---
title: "Springboot+react"
categories: Springboot react settings
last_modified_at: 2020-08-09
---

# 스프링부트 + 리액트 설정


<br>
<br>
<br>

## 1. spring 프로젝트 생성


![스프링부트만들기](https://i.imgur.com/TkfrUyd.png)

>[https://start.spring.io/](https://start.spring.io/)

### 위의 사이트를 이용해서 spring boot를 생성합니다.
- 생성할 떄 web dependency만 추가해줍니다.
- 다른 IDE에서도 spring 프로젝트를 만들 수 있습니다.


## 2. 간단한 REST API 서버 만들기

### 간단한 REST API 서버를 만들어서 아래의 코드를 추가해줍니다.

```java
package com.work.spbreact.controller;

import java.util.Date;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/api/hello")
    public String hello(){
        return "안녕하세요. HI 현재 서버시간은 "+new Date() +"일까요????. \n";
    }


}
```

### 스프링 부트틀 실행시키면 http://localhost:8080/api/hello 에는 위의 내용이 출력됩니다.


> 안녕하세요. HI 현재 서버시간은 Sun Sep 13 19:49:06 KST 2020일까요????.



## 3. React 설치

### 리액트를 설치하는 것은 create-react-app을 활용해서 설치합니다.


```bash
>npx create-react-app frontend
```

- frontend로 들어가서 (cd frontend)
- 리액트 서버를 실행해줍니다. (yarn start)
- 화면에 리액트 로고가 나오면 성공




## 4. 리액트와 스프링부트의 CORS 문제 해결하기

- 현재 스프링부트는 8080 포트에서 실행되고, React는 3000 포트에서 실행되고 있습니다. 따라서 CROS ( cross origin requests ) 가 발생하게 됩니다. 
- 이를 해결하기 위해 Proxy를 프론트에서 잡아주어야 합니다.

### frontend 폴더의 package.json 파일을 열고 "proxy": "http://localhost:8080",를 추가시킵니다.


```json
"scripts": {
    "start": "node scripts/start.js",
    "build": "node scripts/build.js",
    "test": "node scripts/test.js"
  },

  
  "proxy": "http://localhost:8080",


  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  ```


  - 이후 spring boot서버와 react 서버를 켜고 터미널에서 
  > curl http://localhost:3000/api/hello 

  를 입력해서 확인하면 3000 포트로도 8080 포트의 내용이 나오는 것을 확인 할 수 있습니다.


## 5. React의 App.js를 변경해서 REST API 값을 받고 출력해내기 

- curl을 사용하지 않고 웹 화면에 동기화 시키는 방법

### frontend 폴더의 App.js 를 변경


