---
layout: post
title: "[React] 함수형 컴포넌트와 클래스기반 컴포넌트의 차이점"
date: 2018-10-21 00:30
categories: react
tags: [react]
---
#### 함수형 컴포넌트
순수 자바스크립트 함수를 이용하여 컴포넌트를 정의한 것
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

<br>
#### 클래스기반 컴포넌트
`React.Component` 를 상속받은 클래스를 이용하여 컴포넌트를 정의한 것
```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

<br>
#### 차이점

구분 | 함수형 컴포넌트 | 클래스기반 컴포넌트
--- | --- | ---
장점 | 코드를 간결하게 작성할 수 있다. | N/A
단점 | state를 갖지 못하므로 setState 사용불가<br> [life-cycle 함수][1] 사용 불가 | N/A


<br>
#### Ref.
<https://medium.com/@Zwenza/functional-vs-class-components-in-react-231e3fbd7108>


[1]:https://min9nim.github.io/2018/07/react-lifecycle/