---
layout: post
title:  "[nodejs] import 구문 사용"
date:   2019-02-14 00:10
categories: nodejs
tags: [nodejs]
---
노드에서 import 구문을 사용하고자 할 경우 세팅 방법

<br>

#### @babel/preset-env 설치
```
npm install --save-dev @babel/preset-env
```

<br>

#### .babelrc 설정
```
{
    "presets": ["@babel/preset-env"]
}
```

<br>

#### 테스트
[babel-node][1] 를 이용하면 컴파일과 동시에 바로 실행할 수 있다
```
npx babel-node test.js
```


<br>

#### Ref.
<https://babeljs.io/docs/en/babel-preset-env>



[1]:https://babeljs.io/docs/en/babel-node