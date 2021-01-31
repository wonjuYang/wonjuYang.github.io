---
title: "react_native 맛보기 6"
categories: react_native react app
date: 2021-01-31
last_modified_at: 2021-01-31
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 리액트 네이티브 Modal 기능 추가하기

<br/>
<br/>

> [ 리액트 네이티브 Modal 기능 추가하기 ](https://dev-pengun.tistory.com/entry/%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%EB%B6%80%ED%84%B0-%EC%8A%A4%ED%86%A0%EC%96%B4-%EC%B6%9C%EC%8B%9C%EA%B9%8C%EC%A7%80-%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-7-%EC%84%A4%EC%A0%95-Modal-%EA%B8%B0%EB%8A%A5-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0)


# Modal 기능 추가
<br/><br/>

## 1. 삼항 연산자
<br/>

```javascript

{ this.state.settingModal ? <Setting/> : <></> }

```

<br/>

### state에 따라서 달라지는 화면 표현

<br/>

[참고 블로그](https://yuddomack.tistory.com/entry/4React-Native-State%EC%99%80-Props-1%EB%B6%80State)


<br/>
<br/>


<br/><br/>

## 2. onPress에 함수 추가하기

```javascript
<TouchableOpacity onPress={()=>this.toggleSettingModal()}>
```



<br/>
화살표 함수를 활용해서 터치하면 불러올 함수를 명시

<br/><br/><br/><br/>


## 3. 부모 컴포넌트(App.js)의 값을 자식 컴포넌트에(Setting.js)에 전달

### props를 이용

<br/>

settingModal의 state는 App.js에 정의되어있지만, 모달창의 외부를 누르는 버튼은 Setting.js에 정의되어있기 때문에, App.js에서 정의한 toggleSettingModal이라는 함수를 사용할 수 없습니다.

따라서

<br/>

```javascript

//App.js
 <Setting  modalHandler={()=>this.toggleSettingModal()} />


```

<br/>


```javascript

//Setting.js
<TouchableOpacity 
          style={styles.background} 
          activeOpacity={1} //activeOpacity추가 (눌렀을 떄 깜빡이는 효과 제거)
          onPress={this.props.modalHandler}/>
```







<br/><br/>



## 4. AsyncStorage

### AsyncStorage를 이용해서 기기내에 타이틀과 날짜를 저장



```javascript


//저장한 것 불러오는 코드
//UNSAFE_componentWillMount 는 컴포넌트가 마운트 되기 전 호출하는 함수
 async UNSAFE_componentWillMount() {
      try {
        const ddayString = await AsyncStorage.getItem('@dday');
        if(ddayString === null){
          this.setState(
            {
              dday: new Date(),
              ddayTitle: '',
            }
          );
        } else {
          const dday = JSON.parse(ddayString);
          this.setState(
            {
              dday: new Date(dday.date),
              ddayTitle: dday.title,
            }
          );
        }
      } catch(e) {
        console.log("ERR");
      }
  }




  //저장루틴 코드
  //settingHandler 안에서 동작 -> 완료 버튼을 누를 떄 시행
    try {
        const dday = {
            title: title,
            date: date,
        }
        const ddayString = JSON.stringify(dday);
        await AsyncStorage.setItem('@dday', ddayString);
    } catch (e) {
        console.log(e);
    }



```

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
            ddayTitle:'테스트 디데이',
            chatLog:[],
            settingModal:false,
        }
    }


    async UNSAFE_componentWillMount(){
        try{
            const ddayString = await AsyncStorage.getItem('@dday')
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

```javascript

//Setting.js
import React from 'react';
import {View, StyleSheet, Text, TextInput, TouchableOpacity} from 'react-native';
import DatePicker from 'react-native-date-picker';


export default class Setting extends React.Component{

    constructor(props){

        super(props);
        this.state = {
            title:'',
            date: new Date(),
        }

    }


    render(){
        return (
            <View style={styles.container}>
                <TouchableOpacity style={styles.background}
                                  activeOpacity={1}
                                  onPress={this.props.modalHandler}
                />
                <View style={styles.modal}>
                    <Text style={styles.titleText}>설정</Text>
                    <TextInput
                        style={styles.ddayInput}
                        value={this.state.title}
                        onChangeText={(changedText)=>{this.setState({title:changedText})}}
                        placeholder={"디데이 제목을 입력하세요"}
                    />
                    <DatePicker
                        date={this.state.date}
                        onDateChange={(date)=>{this.setState({date:date})}}
                        mode="date"/>
                    <TouchableOpacity onPress={()=>this.props.settingHandler(this.state.title, this.state.date)}>
                        <Text style={styles.doneText}> 완료 </Text>
                    </TouchableOpacity>
                </View>
            </View>
        );
    }

}

const styles = StyleSheet.create({
    container:{
        position:'absolute',
        height: '100%',
        width: '100%',
        backgroundColor:'transparent',
    },
    background:{
        position:'absolute',
        height : '100%',
        width: '100%',
        backgroundColor:'rgba(0, 0, 0, 0.5)'
    },
    ddayInput:{
        backgroundColor:'white',
        marginBottom: 20,
        width: '75%',
        height:40,
        borderBottomWidth:1,
        borderBottomColor:'#a5a5a5',
    },
    modal:{
        marginHorizontal:20,
        borderRadius:10,
        alignItems:'center',
        marginTop:'50%',
        backgroundColor:'white',
    },
    doneText:{
        color:'rgb(1, 123, 255)',
        fontSize:15,
        margin:10
    },
    titleText:{
        fontSize:18,
        margin:10
    }
});
```



<br/>


## 주요 개념 
### onPress
### props
### async


<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/OYOAUi9.png" width=500>



