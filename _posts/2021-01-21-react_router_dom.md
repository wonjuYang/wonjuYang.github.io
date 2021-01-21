---
title: "react-router-dom 쓰는 법"
categories: react react-router-dom
date: 2021-01-21
last_modified_at: 2021-01-21
---



<br/><br/><br/>


# react-router-dom 쓰는 법


1. $ npm install --save react-router-dom 명령으로 깔기

2. App.js 위에 import 하기

import { HashRouter, Route } from 'react-router-dom';

3. route 폴더에 있는 거 import 하기 ex) import Home from './routes/Home';

4. 경로 지정해서 HashRouter 안에 Route 태그로 넣어주기


```javascript

function App() {

  return (  

    <HashRouter>

        <Route path="/" exact={true} component = { Home} />

    </HashRouter>

  );

}



```