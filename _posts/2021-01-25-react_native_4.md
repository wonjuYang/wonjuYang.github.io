---
title: "react_native 맛보기 4"
categories: react_native react app
date: 2021-01-25
last_modified_at: 2021-01-25
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 레이아웃 구성하기 2

<br/>
<br/>

> [ 레이아웃 구성하기 2 ](https://dev-pengun.tistory.com/entry/%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%EB%B6%80%ED%84%B0-%EC%8A%A4%ED%86%A0%EC%96%B4-%EC%B6%9C%EC%8B%9C%EA%B9%8C%EC%A7%80-%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-4-%EB%A0%88%EC%9D%B4%EC%95%84%EC%9B%83-%EA%B5%AC%ED%98%84-%EB%A7%88%EB%AC%B4%EB%A6%AC%ED%95%98%EA%B8%B0)


# 리엑트 네이티브 레이아웃 구성하기 2
<br/><br/>

## 1. 배경 넣기
<br/>
backgroundImage 컴포넌트로 배경 이미지 넣기<br/>
> 배경 이미지 넣을 때 옵션이 많을텐데 기본으로 뭐가 적용되고 있을까?


<br/><br/>

## 2. flex (정렬)
<br/>
flexDirection 이 새로 나왔다. 항상 헷깔리는 개념인데 
[ 공식 문서 ](https://reactnative.dev/docs/flexbox)
 를 참고하면 천하무적이다.
<br/><br/><br/><br/>



처음 css 배울 때 재미있게 했던 게구리 게임! 온 수강생들이 다들 붙어서 재미있게 했었다
> [ 개구리 게임 ](https://flexboxfroggy.com/#ko)


<br/><br/>

```javascript
//App.js
import React from 'react';
import { StyleSheet, Text, View, Image, TextInput, TouchableOpacity, ScrollView,
    ImageBackground } from 'react-native';

export default class App extends React.Component {
    render(){
        return (
            <View style={styles.container}>
                <ImageBackground style={styles.background} source={require('./images/background.png')}>
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
                        <ScrollView style={styles.chatScrollView}>

                        </ScrollView>
                        <View style={styles.chatControl}>
                            <TextInput style={styles.chatInput}/>
                            <TouchableOpacity style={styles.sendButton}>
                                <Text>
                                    전송
                                </Text>
                            </TouchableOpacity>
                        </View>
                    </View>
                </ImageBackground>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container:{
        flex:1,
    },
    background:{
        width:'100%',
        height:'100%',
    },
    settingView:{
         flex:1,
         justifyContent:'center',
         alignItems:'flex-end',
         marginRight:'1%',
    },
    ddayView:{
         flex:5,
         justifyContent:'center',
         alignItems : 'center',
    },
    chatView:{
         flex:7,
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
    sendButton:{
        backgroundColor:'rgb(97, 99, 250)',
        height:40,
        width:50,
        borderRadius:20,
        padding:5,
        justifyContent:'center',
        alignItems:'center',
        marginLeft:5,
    },
    chatInput:{
        backgroundColor:'white',
        width:'75%',
        height:40,
        borderWidth:1,
        borderColor:'#a5a5a5',
        borderRadius:20,
    },
    chatControl:{
        flexDirection:'row',
        alignItems:'center',
        justifyContent:'center',
        marginBottom:5,
        marginTop:10,
    },
    chatScrollView:{
        width:'90%',
        alignSelf:'center',
        backgroundColor:'rgba(201,201,201,0.7)',
        borderRadius:5,
        borderWidth:1,
        borderColor:'#a5a5a5',

    },
});
```



<br/>


## 주요 개념 
### BackgroundImage


<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/47Qdzeh.png" width=500>



