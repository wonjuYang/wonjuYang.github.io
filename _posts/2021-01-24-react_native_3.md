---
title: "react_native 맛보기 3"
categories: react_native react app
date: 2021-01-24
last_modified_at: 2021-01-24
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 레이아웃 구성하기

<br/>
<br/>

> [ 레이아웃 구성하기 ](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-3-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0)


# 리엑트 네이티브 레이아웃 구성하기
<br/><br/>

## 1. 터치 영역
<br/>
TouchableOpacity는 자신이 감싼 범위의 컴포넌트를 터치할 수 있는 버튼으로 만들어주는 역할

<br/><br/>

## 2. flex (정렬)
<br/>
정렬은 그동안 배웠던 개념이랑 거의 다 유사해서 바로 배울 수 있었다. 항상 헷깔리는 개념인데 
[ 공식 문서 ](https://reactnative.dev/docs/flexbox)
 를 참고하면 천하무적이다.
<br/><br/><br/><br/>



처음 css 배울 때 재미있게 했던 게구리 게임! 온 수강생들이 다들 붙어서 재미있게 했었다
> [ 개구리 게임 ](https://flexboxfroggy.com/#ko)


<br/><br/>

```javascript
//App.js
import React from 'react';
import { StyleSheet, Text, View, Image, TextInput, TouchableOpacity, ScrollView
 } from 'react-native';

export default class App extends React.Component {
    render(){
        return (
            <View style={styles.container}>
                <View style={styles.settingView}>
                    <TouchableOpacity>
                        <Image source={require('./icon/setting.png')}/>
                    </TouchableOpacity>
                </View>
                <View style={styles.ddayView}>
                    <Text style={styles.titleText}>
                        수능까지
                    </Text>
                    <Text style={styles.ddayText}>
                        D-123
                    </Text>
                    <Text style={styles.dateText}>
                        2021년 11월 11일
                    </Text>
                </View>
                <View style={styles.chatView}>
                    <ScrollView>

                    </ScrollView>
                    <TextInput/>
                    <TouchableOpacity>
                        <Text>
                            전송
                        </Text>
                    </TouchableOpacity>
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
         backgroundColor:'red',
         justifyContent:'center',
         alignItems:'flex-end',
         marginRight:'1%',
    },
    ddayView:{
         flex:6,
         backgroundColor:'green',
         justifyContent:'center',
         alignItems : 'center',
    },
    chatView:{
         flex:6,
         backgroundColor:'blue'
    },
    titleText:{
        alignSelf:'flex-end',
        fontSize:36,
        fontWeight:'bold',
        color:'#4A4A4A',
        marginRight:'15%',
    },
    ddayText:{
        fontSize:100,
        fontWeight:'bold',
        color:'#4A4A4A'

    },
    dateText:{
        alignSelf:'flex-start',
        fontSize:21,
        fontWeight:'bold',
        color:'#4A4A4A',
        marginLeft:'15%',
    },
});
```



<br/>

## 주요 개념 
### TouchableOpacity!
### justifyContent, alignItems, alignSelf
### margin 개념들



<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/OKPK5dd.png" width=500>



