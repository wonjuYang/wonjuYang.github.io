---
title: "react_native 맛보기 2"
categories: react_native react app
date: 2021-01-23
last_modified_at: 2021-01-23
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 컴포넌트와 메인 화면 분활

<br/>
<br/>

> [ 컴포넌트와 메인 화면 분활 ](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-2-Component%EC%99%80-%EB%A9%94%EC%9D%B8%ED%99%94%EB%A9%B4-%EB%B6%84%ED%95%A0);


# 리엑트 네이티브 기본 컴포넌트 
<br/><br/>

## 1. 기본 컴포넌트 배우기
<br/>
대체적으로 하나의 컴포넌트만 최종 리턴되어야 된다는 점과 style 적용 문법 등 react와 비슷한 것들이 많다.

<br/><br/>

```javascript
//App.js
import React from 'react';
import { StyleSheet, Text, View, Image, TextInput } from 'react-native';

export default class App extends React.Component {
    render(){
        return (
            <View style={styles.container}>
                <Image
                    style={% raw %} {{width:50, height:50}} {% endraw %} 
                    source={% raw %}{{uri: 'https://facebook.github.io/react-native/img/tiny_logo.png'}} {% endraw %} 
                />
                <TextInput/>
                <Text style={styles.loadingText}>
                    Now Loading...
                </Text>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container:{
        backgroundColor:'gold',
    },
    loadingText:{
        fontSize: 45,
    }
});

```



<br/>

# 성공!!

<img src="https://i.imgur.com/DZRwyw3.png" width=500>

<br/><br/><br/>


## 2. 메인 화면 구현


<br/>


```javascript

//App.js
import React from 'react';
import { StyleSheet, Text, View, Image, TextInput } from 'react-native';

export default class App extends React.Component {
    render(){
        return (
            <View style={styles.container}>
                <View style={styles.settingView}>

                </View>
                <View style={styles.ddayView}>

                </View>
                <View style={styles.chatView}>

                </View>

            </View>
        );
    }
}

const styles = StyleSheet.create({
    container:{
        flex:1,
    },
    settingView:{
         flex:1,
         backgroundColor:'red'
    },
    ddayView:{
         flex:6,
         backgroundColor:'green'
    },
    chatView:{
         flex:6,
         backgroundColor:'blue'
    },
});
```

## 주요 개념 
### flex : 화면을 차지하는 비율 설정(세로) 
### container는 현재 화면 전체를 차지 1 
### 각 view는 이 container에서 1 : 6 : 6 비율로 화면 차지



<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/ci7JPyB.png" width=500>



