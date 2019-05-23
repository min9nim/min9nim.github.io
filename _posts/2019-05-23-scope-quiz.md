---
layout: post
title:  "[js] 자바스크립트 scope 퀴즈"
date:   2019-05-23 00:10
categories: js
tags: [js]
---
자바스크립트의 함수단위 스코프, 동적 this 바인딩, lexical scope 등 자바스크립트에서 scope 에 대한 개념을 정확히 이해하기 위해 알아야 할 사항들은 상당히 많다.

특별히 아래 퀴즈들을 통해 나는 자바스크립트 scope 에 대하 정확한 이해를 하고 있는가 점검해 보도록 하자

```javascript
var name = 'global'

function fn(){
  console.log(this.name)
}    

class Outer {
  name = 'object property'
  Inner(){
    var name = 'inner of local'
    console.log(this.name)
    fn()
  }
}

new Outer().Inner()
```
실행결과는?

아래와 같다
```
object property
global
```

this 는 해당 함수가 실행되는 모양?에 따라 동적으로 바인딩된다. 객체의 메소드로서 호출될 때 this는 해당 객체가 되고 함수로서 직접 호출될 때는 글로벌객체에 바인딩된다.

<br>

fn 함수가 Inner 안에서 정의되면 어떨까
```javascript
var name = 'global'

class Outer {
  name = 'object property'
  Inner(){
    var name = 'inner of local'
    console.log(this.name)
    function fn(){
      console.log(this.name)
    }    
    fn()
  }
}

new Outer().Inner()
```

```
object property
Uncaught TypeError: Cannot read property 'name' of undefined
    at fn (<anonymous>:9:24)
    at Outer.Inner (<anonymous>:11:5)
    at <anonymous>:15:13
```
클래스의 body는 자동으로 strict 모드로 실행된다.
strict 모드에서는 함수로 호출될 때 내부 this 가 글로벌객체에 바인딩되지 않고 undefined 가 되기 때문에 오류가 발생한다.

<br>

Outer 를 함수로 바꾸면 어떻게 될까
```javascript
var name = 'global'

function Outer() {
  var name = 'object property'
  function Inner(){
    var name = 'inner of local'
    console.log(this.name)
    function fn(){
      console.log(this.name)
    }    
    fn()
  }
  Inner()
}

Outer()
```

```
global
global
```
fn과 Inner 가 모두 함수로서 호출되었기 때문에 this 는 글로벌객체에 바인딩된다(strict mode 라면 undefined)




Inner 를 화살표함수로 변경하면??
```javascript
var name = 'global'

function Outer() {
  var name = 'object property'
  var Inner = () => {
    var name = 'inner of local'
    console.log(this.name)
    function fn(){
      console.log(this.name)
    }    
    fn()
  }
  Inner()
}

Outer()
```

```
global
global
```
화살표함수를 사용하더라도 마찬가지로 Inner와 fn 이 함수로서 호출되었기 때문에 this 는 전역객체에 바인딩 된다
