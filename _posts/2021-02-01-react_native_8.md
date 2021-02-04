---
title: "react_native 맛보기 7"
categories: react_native react app
date: 2021-02-01
last_modified_at: 2021-02-01
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 리액트 네이티브 메모 구현하기

<br/>
<br/>

> [ 리액트 네이티브 메모 구현하기 ](https://dev-pengun.tistory.com/entry/8-%EC%B1%84%ED%8C%85%EA%B8%B0%EB%8A%A5-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%EB%B6%80%ED%84%B0-%EC%8A%A4%ED%86%A0%EC%96%B4-%EC%B6%9C%EC%8B%9C%EA%B9%8C%EC%A7%80-%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native)


# 메모 구현

채팅이라기보다는 메모에 가까워서 메모 구현하기로 써봤다

<br/><br/>

## 1. AsyncStorage를 사용한 저장
<br/>

```javascript

chatHandler() {
    this.setState({
      chatLog: [ ...this.state.chatLog, this.makeDateString() + ' : ' + this.state.chatInput],
      chatInput: '',
    },async ()=>{
      const chatLogString = JSON.stringify(this.state.chatLog);
      await AsyncStorage.setItem('@chat', chatLogString);
    });
  }

```

<br/>

### asyncStorage 삭제

<br/>

삭제하는 방법이 궁금해서 찾아서 적용해 보았다

```javascript
<TouchableOpacity
    onPress={()=>AsyncStorage.clear()}>
    <Text>
        삭제
    </Text>
</TouchableOpacity>
```

### cf)특정 key 삭제하는 법

```javascript
async removeItemValue(key) {
    try {
        await AsyncStorage.removeItem(key);
        return true;
    }
    catch(exception) {
        return false;
    }
}
```



<br/>
<br/>


<br/><br/>

## 2. map 함수로 뿌려주기

```javascript
<ScrollView style={styles.chatScrollView}>
    {this.state.chatLog.map((chat)=>{
        return <Text style={styles.chat}>{chat}</Text>
    })}
</ScrollView>
```

<br/><br/><br/><br/>

```javascript
//App.js
import React from 'react';
import { StyleSheet, Text, View, Image, TextInput, TouchableOpacity, ScrollView,
    ImageBackground } from 'react-native';

     import AsyncStorage from '@react-native-async-storage/async-storage';
     import Setting from './Setting.js';


     export default class App extends React.Component {
         constructor(props){
             super(props);
             this.state = {
                 dday:new Date(),
                 today:new Date(),
                 ddayTitle:'',
                 chatInput:'',
                 chatLog:[],
                 settingModal:false,
             }
         }


    async UNSAFE_componentWillMount(){
        try{
            const ddayString = await AsyncStorage.getItem('@dday')
            const chatLogString = await AsyncStorage.getItem('@chat');


            if(chatLogString == null){
                this.setState({chatLog:[]});
            }else {

                const chatLog = JSON.parse(chatLogString);
                this.setState({chatLog:chatLog});
            }

            if(ddayString == null){
                this.setState(
                    {
                        dday:new Date(),
                        ddayTitle:'',
                    }
                );
            }else{
                const dday = JSON.parse(ddayString);
                this.setState(
                    {
                        dday:new Date(dday.date),
                        ddayTitle:dday.title,
                    }
                );
            }
        } catch(e){
            console.log("ERR")
        }
    }

    toggleSettingModal(){
        this.setState({
            settingModal:!this.state.settingModal
        })
    }

    chatHandler(){
        this.setState({
            chatLog:[ ...this.state.chatLog, this.makeDateString2() + ':' + this.state.chatInput],
            chatInput:'',
        }, async()=>{
            const chatLogString = JSON.stringify(this.state.chatLog);
            await AsyncStorage.setItem('@chat', chatLogString);
        })
    }





    async settingHandler(title, date) {
        this.setState({
            ddayTitle: title,
            dday: date,
        });

        try{
            const dday = {
                title : title,
                date : date,
            }
            const ddayString = JSON.stringify(dday);
            await AsyncStorage.setItem('@dday', ddayString);


        } catch(e){
            console.log(e);
        }

        this.toggleSettingModal();
    }


    makeDateString(){
        return this.state.dday.getFullYear() + '년' +
                (this.state.dday.getMonth()+1) + '월' +
                this.state.dday.getDate() + '일';
    }



    makeDateString2(){
        return this.state.today.getFullYear() + '년' +
                (this.state.today.getMonth()+1) + '월' +
                this.state.today.getDate() + '일';
    }



    makeRemainString() {
        const distance = new Date().getTime() - this.state.dday.getTime();
        console.log(new Date(), this.state.dday,distance / (1000 * 60 * 60 * 24) )
        const remain = Math.floor(distance / (1000 * 60 * 60 * 24));
        if(remain < 0) {
            return 'D'+remain;
        } else if (remain > 0) {
            return 'D+'+remain;
        } else if (remain === 0) {
            return 'D-day';
        }
    }



    render(){
        return (
            <View style={styles.container}>
                <ImageBackground style={styles.background} source={require('./images/background.png')}>
                    <View style={styles.settingView}>
                        <TouchableOpacity onPress={()=>this.toggleSettingModal()}>
                            <Image source={require('./icon/setting.png')}/>
                        </TouchableOpacity>
                    </View>
                    <View style={styles.ddayView}>
                        <Text style={styles.titleText}>
                            {this.state.ddayTitle}까지
                        </Text>
                        <Text style={styles.ddayText}>
                            {this.makeRemainString()}
                        </Text>
                        <Text style={styles.dateText}>
                            {this.makeDateString()}
                        </Text>
                    </View>
                    <View style={styles.chatView}>
                        <ScrollView style={styles.chatScrollView}>
                            {this.state.chatLog.map((chat)=>{
                                return <Text style={styles.chat}>{chat}</Text>
                            })}
                        </ScrollView>
                        <View style={styles.chatControl}>
                            <TextInput style={styles.chatInput}
                                        value={this.state.chatInput}
                                        onChangeText={(changedText)=>{
                                            this.setState({chatInput: changedText})
                                        }}/>
                            <TouchableOpacity style={styles.sendButton}
                                                onPress={()=>this.chatHandler()}>
                                <Text>
                                    전송
                                </Text>
                            </TouchableOpacity>
                            <TouchableOpacity
                                onPress={()=>AsyncStorage.clear()}>
                                <Text>
                                    삭제
                                </Text>
                            </TouchableOpacity>

                        </View>
                    </View>
                   {this.state.settingModal ?
                               <Setting
                                 modalHandler={()=>this.toggleSettingModal()}
                                 settingHandler={(title, date)=>this.settingHandler(title, date)}/>
                             : <></> }
                </ImageBackground>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container:{
        flex:1,
    },
    chat:{
        fontSize:18,
        fontWeight:'bold',
        color:'#4A4A4A',
        margin:2,
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
### asyncStorage
### map



<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/sWHALQM.png" width=500>



