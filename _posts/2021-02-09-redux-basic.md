---
title: "리덕스 기초 CRUD by 생활코딩"
categories: boostcourse kotlin
date: 2021-02-09
last_modified_at: 2021-02-09
---


<br/>
<br/>
<br/>


# Redux : A predictable state container for Javascript App

# 자바스크립트로 만든 애플리케이션들을 위한 예측가능한 상태의 저장소

# 복잡성 : 눈에 보이지 않기 때문에 가장 위험함

# 리덕스는 애플리케이션의 복잡성을 낮추기 위해 우리의 코드가 어떤 결과를 가져올지 예측 가능하게 만들어 준다

# 어떻게 가능한가?


# 1. Single Source of Truth


## 하나의 상태를 갖는다
상태 = 객체<br/>
하나의 객체에 모든 데이터를 우겨 넣는다 <br/>
한곳에 데이터를 중앙집중적으로 관리<br/>
훨씬 더 데이터를 관리하기 쉬워짐<br/>

## 이상태는 너무나 중요해서 외부로부터 철저히 분리시킴
인가된 담당자(함수)만을 통해서 할 수 있다<br/>
데이터를 쓰고 싶어도 직접 못 쓰고 dispatcher나 reducer를 통해서만 데이터에 접근해서 바꾸기 가능<br/>
데이터를 가져올 떄도 getState라는 함수를 사용해서 가져올 수 있다<br/>


# 2. state값이 바뀔 때마다 지령을 내리는 함수 존재 


## Undo와 Redo를 간편하게 가능
각각의 state값들을 철저히 통제 데이터를 바꿀 때 원본을 복제하고 복제한 것을 바꿔서 새로운 것으로 채택함<br/>
각각의 상태 변화가 서로에게 영향을 전혀 주지 않는 독립된 상태 유지<br/>
이러한 상태를 잘 이용하면 undo redo를 매우 쉽게 처리 가능<br/>

## 이전의 상태 까지도 꼼꼼하게 recording 가능
debugger를 통해 어플리케이션의 현재 상태를 보는데 redux를 사용하면 이전의 상태까지도 기록하여<br/>
과거의 어떤 시점에 찾아가서 문제 해결을 좀 더 쉽게 할 수 있도록 도와줌<br/>


##  hot module reloading : 모듈 리로딩 코드를 작성하면 자동으로 어플리케이션에 적용됨 
데이터가 보통은 수정되면 데이터가 사라짐 그러나 리덕스에을 사용하면 코드는 바꼈는데 데이터는 남아있는 상태로 테스트 가능<br/>



</br></br></br></br></br>





# 리덕스 없이 컴포넌트 변경

```html

<html>
    <body>
        <style>
            .container{
                border: 5px solid black;
                padding: 10px;

            }

        </style>
        <div id="red"></div>
        <div id="green"></div>
        <div id="blue"></div>
        <script>

            function red(){

                document.querySelector('#red').innerHTML = 
                `
                    <div class="container" id="component_red">
                        <h1>red</h1>
                        <input type="button" value="fire" onclick="
                            document.querySelector('#component_red').style.backgroundColor= 'red';
                            document.querySelector('#component_green').style.backgroundColor= 'red';
                            document.querySelector('#component_blue').style.backgroundColor= 'red';
                        "/>
                    </div>
                `
            }
            red();

            function green(){

                document.querySelector('#green').innerHTML = 
                `
                    <div class="container" id="component_green">
                        <h1>green</h1>
                        <input type="button" value="fire" onclick="
                            document.querySelector('#component_red').style.backgroundColor= 'green';
                            document.querySelector('#component_green').style.backgroundColor= 'green';
                            document.querySelector('#component_blue').style.backgroundColor= 'green';
                        "/>
                    </div>
                `
            }
            green();

            function blue(){

                document.querySelector('#blue').innerHTML = 
                `
                    <div class="container" id="component_blue">
                        <h1>blue</h1>
                        <input type="button" value="fire" onclick="
                            document.querySelector('#component_red').style.backgroundColor= 'blue';
                            document.querySelector('#component_green').style.backgroundColor= 'blue';
                            document.querySelector('#component_blue').style.backgroundColor= 'blue';
                        "/>
                    </div>
                `
            }
            blue();

        </script>

    </body>


</html>

```


</br></br>

## 컴포넌트가 추가될 때마다 다시 이전 컴포넌트로 돌아가서 새 컴포넌트에 대한 설정을 해야 한다

</br></br></br></br></br>



# 리덕스를 활용한 컴포넌트 변경


```html

<html>
    <head>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.0.1/redux.js"></script>
    </head>
    <body>
        
    </body>
        <style>
            .container{
                border: 5px solid black;
                padding: 10px;

            }

        </style>
        <div id="red"></div>
        <div id="blue"></div>
        <div id="green"></div>
        <script>    
            function reducer(state, action){
                console.log(state, action)
                if(state === undefined){
                    return {color:'yellow'}
                }
                var newState; //이전 상태를 보존하기 위해 newState를 통해 바꿔주는 것
                if(action.type === 'CHANGE_COLOR'){
                    newState = Object.assign({}, state, {color:action.color});
                }
                return newState;
            }

            var store = Redux.createStore(
                reducer,
                window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__() //크롬에서 redux 확장프로그램 쓰려고
            );

            function red(){
                var state = store.getState();
                document.querySelector('#red').innerHTML = 
                `
                    <div class="container" id="component_red" style="background-color:${state.color}">
                        <h1>red</h1>
                        <input type="button" value="fire" onclick="
                           store.dispatch({type:'CHANGE_COLOR', color:'red'});
                        "/>
                    </div>
                `;
            }
            store.subscribe(red);
            red();

            function blue(){
                var state = store.getState();
                document.querySelector('#blue').innerHTML = 
                `
                    <div class="container" id="component_blue" style="background-color:${state.color}">
                        <h1>blue</h1>
                        <input type="button" value="fire" onclick="
                           store.dispatch({type:'CHANGE_COLOR', color:'blue'});
                        "/>
                    </div>
                `;
            }
            store.subscribe(blue);
            blue();

            function green(){
                var state = store.getState();
                document.querySelector('#green').innerHTML = 
                `
                    <div class="container" id="component_green" style="background-color:${state.color}">
                        <h1>green</h1>
                        <input type="button" value="fire" onclick="
                           store.dispatch({type:'CHANGE_COLOR', color:'green'});
                        "/>
                    </div>
                `;
            }

            store.subscribe(green);
            green();

            

        </script>

    </body>


</html>

```

</br></br>

## 컴포넌트가 추가되어도 현재의 컴포넌트에 집중 가능
## action -> dispatch -> reducer -> state변경 -> subscribe -> render 


</br></br></br></br></br>

# redux 를 활용한 CRUD

</br>

## 강의에서 소개된 CRD까지의 코드

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.0.1/redux.js"></script>
    </head>
    <body>
        <div id="subject"></div>
        <div id="toc"></div>
        <div id="contorl"></div>
        <div id="content"></div>
        <script>
            function subject(){
                document.querySelector('#subject').innerHTML = `
                <header>
                    <h1>WEB</h1>
                    Hello, WEB!
                </header>
                `
            }
            function TOC(){
                var state = store.getState();
                var i = 0;
                var liTags = '';
                while(i<state.contents.length){
                    liTags += `
                        <li>
                            <a onclick="
                                event.preventDefault();
                                var action = {type:'SELECT', id:${state.contents[i].id}}
                                store.dispatch(action);
                            " href="${state.contents[i].id}">
                                ${state.contents[i].title}
                            </a>
                        </li>
                    `
                    i = i + 1;
                }
                document.querySelector('#toc').innerHTML = `
                <nav>
                    <ol>
                        ${liTags}
                    </ol>
                </nav>
                `
            }
            function control(){
                document.querySelector('#contorl').innerHTML = `
                <ul>
                    <li><a onclick="
                        event.preventDefault();
                        store.dispatch({
                            type:'CHANGE_MODE',
                            mode:'create'
                        })
                        " href="/create">create</a></li>
                    <li><input onclick="
                            store.dispatch({
                                type:'DELETE',
                            })
                        " type="button" value="delete"></li>
                </ul>
                `
            }
            function article(){
                var state = store.getState();
                if(state.mode === 'create'){
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <form onsubmit="event.preventDefault(); 
                        var _title = this.title.value;
                        var _desc = this.desc.value;
                        store.dispatch({
                            type:'CREATE', title:_title, desc:_desc 
                        })">
                            <p>
                                <input type="text" name="title"
                                placeholder="title">    
                            </p>
                            <p>
                                <textarea name="desc"
                                placeholder="description"></textarea>    
                            </p>    
                            <p>
                                <input type="submit">    
                            </p>
                        </form>
                    </article>
                    `
                }else if(state.mode === 'read'){
                    var i = 0;
                    var aTitle, aDesc;
                    while( i < state.contents.length){
                        if(state.contents[i].id === state.selected_id){
                            aTitle = state.contents[i].title;
                            aDesc = state.contents[i].desc;
                            break;
                        }
                        i = i+1;
                    }
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <h2>${aTitle}</h2>
                        ${aDesc}
                    </article>
                    `
                }else if(state.mode === 'welcome'){
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <h2>Delete finish</h2>
                    </article>
                    `
                }
                
            }
            function reducer(state, action){
                
                if(state === undefined){
                    return {
                        max_id:3,
                        mode:'read',
                        selected_id:1,
                        contents:[
                            {id:1, title:'HTML2',desc:'HTML is..'},
                            {id:2, title:'CSS',desc:'CSS is..'},
                            {id:3, title:'javascript',desc:'javascript is..'},
                        ]
                    }
                }
                var newState ={};
                if(action.type === 'SELECT'){
                    newState = Object.assign({}, state, {selected_id:action.id, mode:'read'});
                }else if(action.type === 'CREATE'){
                    var newMaxId = state.max_id + 1;
                    var newContents = state.contents.concat();
                    newContents.push({id:newMaxId, title:action.title, desc:action.desc});
                    newState = Object.assign({}, state, {
                        max_id:newMaxId,
                        contents:newContents,
                        mode:'read',
                        selected_id:newMaxId,
                    })
                }else if(action.type === 'DELETE'){
                    var newContents = [];
                    var i = 0;
                    while(i < state.contents.length){
                        if(state.selected_id !== state.contents[i].id){
                            newContents.push(
                                state.contents[i]
                            );
                        }
                        i = i+1;
                    }
                    newState = Object.assign({}, state, {
                        contents:newContents,
                        mode:'welcome',
                        max_id:state.max_id-1
                    })
                }else if(action.type === 'CHANGE_MODE'){
                    newState = Object.assign({}, state, {
                        mode:action.mode
                    })
                }
                console.log(action, state, newState);
                return newState;
            }
            var store = Redux.createStore(reducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());
            store.subscribe(article);
            store.subscribe(TOC);
            subject();
            TOC();
            control();
            article();
        </script>


        

    </body>
<body>
    
</body>
</html>

```

</br></br>


## 내가 U를 추가해서 CRUD를 완성한 코드

```html
<!DOCTYPE html>
<html>
    <head>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.0.1/redux.js"></script>
    </head>
    <body>
        <div id="subject"></div>
        <div id="toc"></div>
        <div id="contorl"></div>
        <div id="content"></div>
        <script>
            function subject(){
                document.querySelector('#subject').innerHTML = `
                <header>
                    <h1>WEB</h1>
                    Hello, WEB!
                </header>
                `
            }
            function TOC(){
                var state = store.getState();
                var i = 0;
                var liTags = '';
                while(i<state.contents.length){
                    liTags += `
                        <li>
                            <a onclick="
                                event.preventDefault();
                                var action = {type:'SELECT', id:${state.contents[i].id}}
                                store.dispatch(action);
                            " href="${state.contents[i].id}">
                                ${state.contents[i].title}
                            </a>
                        </li>
                    `
                    i = i + 1;
                }
                document.querySelector('#toc').innerHTML = `
                <nav>
                    <ol>
                        ${liTags}
                    </ol>
                </nav>
                `
            }
            function control(){
                document.querySelector('#contorl').innerHTML = `
                <ul>
                    <li><a onclick="
                        event.preventDefault();
                        store.dispatch({
                            type:'CHANGE_MODE',
                            mode:'create'
                        })
                        " href="/create">create</a></li>
                    <li><a onclick="
                        event.preventDefault();
                        store.dispatch({
                            type:'CHANGE_MODE',
                            mode:'update'
                        })
                        " href="/update">update</a></li>
                    <li><input onclick="
                            store.dispatch({
                                type:'DELETE',
                            })
                        " type="button" value="delete"></li>
                </ul>
                `
            }
            function article(){
                var state = store.getState();
                if(state.mode === 'create'){
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <form onsubmit="event.preventDefault(); 
                        var _title = this.title.value;
                        var _desc = this.desc.value;
                        store.dispatch({
                            type:'CREATE', title:_title, desc:_desc 
                        })">
                            <p>
                                <input type="text" name="title"
                                placeholder="title">    
                            </p>
                            <p>
                                <textarea name="desc"
                                placeholder="description"></textarea>    
                            </p>    
                            <p>
                                <input type="submit">    
                            </p>
                        </form>
                    </article>
                    `
                }else if(state.mode === 'update'){
                    var update_id = state.selected_id;
                    var i = 0;
                    var aTitle, aDesc;
                    while( i < state.contents.length){
                        if(state.contents[i].id === state.selected_id){
                            aTitle = state.contents[i].title;
                            aDesc = state.contents[i].desc;
                            break;
                        }
                        i = i+1;
                    }
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <form onsubmit="event.preventDefault(); 
                        var _title = this.title.value;
                        var _desc = this.desc.value;
                        store.dispatch({
                            type:'UPDATE', title:_title, desc:_desc
                        })">
                            <p>
                                <input type="text" name="title"
                                value=${aTitle}>    
                            </p>
                            <p>
                                <textarea name="desc">${aDesc}</textarea>    
                            </p>    
                            <p>n
                                <input type="submit" value="수정">    
                            </p>
                        </form>
                    </article>
                    `
                }else if(state.mode === 'read'){
                    var i = 0;
                    var aTitle, aDesc;
                    while( i < state.contents.length){
                        if(state.contents[i].id === state.selected_id){
                            aTitle = state.contents[i].title;
                            aDesc = state.contents[i].desc;
                            break;
                        }
                        i = i+1;
                    }
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <h2>${aTitle}</h2>
                        ${aDesc}
                    </article>
                    `
                }else if(state.mode === 'delete_finish'){
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <h2>Delete finish</h2>
                    </article>
                    `
                }
                else if(state.mode === 'update_finish'){
                    document.querySelector('#content').innerHTML = `
                    <article>
                        <h2>update finish</h2>
                    </article>
                    `
                }
                
            }
            function reducer(state, action){
                
                if(state === undefined){
                    return {
                        max_id:3,
                        mode:'read',
                        selected_id:1,
                        contents:[
                            {id:1, title:'HTML2',desc:'HTML2 is..'},
                            {id:2, title:'CSS',desc:'CSS is..'},
                            {id:3, title:'javascript',desc:'javascript is..'},
                        ]
                    }
                }
                var newState ={};
                if(action.type === 'SELECT'){
                    newState = Object.assign({}, state, {selected_id:action.id, mode:'read'});
                }else if(action.type === 'UPDATE'){
                    var newContents = [];
                    var i = 0;
                    while(i < state.contents.length){
                        if(state.selected_id !== state.contents[i].id){
                            newContents.push(
                                state.contents[i]
                            );
                        }else{
                            newContents.push({id:state.selected_id, title:action.title, desc:action.desc});
                        }
                        i = i+1;
                    }
                    newState = Object.assign({}, state, {
                        contents:newContents,
                        mode:'update_finish',
                    })
                }else if(action.type === 'CREATE'){
                    var newMaxId = state.max_id + 1;
                    var newContents = state.contents.concat();
                    newContents.push({id:newMaxId, title:action.title, desc:action.desc});
                    newState = Object.assign({}, state, {
                        max_id:newMaxId,
                        contents:newContents,
                        mode:'read',
                        selected_id:newMaxId,
                    })
                }else if(action.type === 'DELETE'){
                    var newContents = [];
                    var i = 0;
                    while(i < state.contents.length){
                        if(state.selected_id !== state.contents[i].id){
                            newContents.push(
                                state.contents[i]
                            );
                        }
                        i = i+1;
                    }
                    newState = Object.assign({}, state, {
                        contents:newContents,
                        mode:'delete_finish',
                        max_id:state.max_id-1
                    })
                }else if(action.type === 'CHANGE_MODE'){
                        newState = Object.assign({}, state, {
                        mode:action.mode
                    })
                }
                console.log(action, state, newState);
                return newState;
            }
            var store = Redux.createStore(reducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__());
            store.subscribe(article);
            store.subscribe(TOC);
            subject();
            TOC();
            control();
            article();
        </script>


        

    </body>
<body>
    
</body>
</html>
```




