---
title: "react_native 맛보기 5"
categories: react_native react app
date: 2021-01-27
last_modified_at: 2021-01-27
---


<br/><br/><br/>


## 맛보기 참고 블로그

> [리액트 네이티브 참고 블로그](https://dev-pengun.tistory.com/entry/%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%A7%9B%EB%B3%B4%EA%B8%B0)

위의 블로그를 참고하여 리액트 네이티브 기초를 따라할 예정입니다


<br/><br/>

# 리액트 네이티브 State

<br/>
<br/>

> [ 리액트 네이티브 State ](https://dev-pengun.tistory.com/entry/%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%EB%B6%80%ED%84%B0-%EC%8A%A4%ED%86%A0%EC%96%B4-%EC%B6%9C%EC%8B%9C%EA%B9%8C%EC%A7%80-%EB%94%94%EB%8D%B0%EC%9D%B4-%EC%95%B1-%EB%94%B0%EB%9D%BC-%EB%A7%8C%EB%93%A4%EB%A9%B0-%EB%B0%B0%EC%9A%B0%EB%8A%94-React-Native-5-state)


# 리액트 네이티브 State
<br/><br/>

## 1. State
<br/>
리액트는 State와 Props라는 객체를 사용하여 화면에 표시되는 가변적인 값을 관리함<br/>

### state와 props의 특징
1. Props 혹은 State의 값 변경이 감지될 때마다 render()가 수행된다
2. State에는 현재 컴포넌트의 화면을 그리는 것과 관련된 대다수의 값들을 담는다.
3. 데이터의 흐르미은 상위 컴포넌트에서 하위 컴포넌트로 단방향이다
4. Props에는 상위 컴포넌트에서 전달받은 값이 담겨있으며 변경 불가능하다.
5. Props 혹은 State는 비동기적으로 업데이트 될수 있다. 
<br/>

[참고 블로그](https://yuddomack.tistory.com/entry/4React-Native-State%EC%99%80-Props-1%EB%B6%80State)


<br/>
<br/>


<br/><br/>

## 2. 화살표 함수
<br/>
function 표현에 비해 구문이 짧고 익명으로 표현

<br/><br/><br/><br/>



```javascript

//예시


var elements = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

// 이 문장은 배열을 반환함: [8, 6, 7, 9]
elements.map(function(element) {
  return element.length;
});

// 위의 일반적인 함수 표현은 아래 화살표 함수로 쓸 수 있다.
elements.map((element) => {
  return element.length;
}); // [8, 6, 7, 9]

// 파라미터가 하나만 있을 때는 주변 괄호를 생략할 수 있다.
elements.map(element => {
  return element.length;
}); // [8, 6, 7, 9]

```
> [ 화살표 함수 ](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)


<br/><br/>

# 설정 Modal 만들기


<br/><br/>

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
                <TouchableOpacity style={styles.background}/>
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
                        mode="date"/>
                    <TouchableOpacity>
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
### State


<br/><br/><br/>

# 성공!!

<img src="https://i.imgur.com/mq8tS5Z.png" width=500>



