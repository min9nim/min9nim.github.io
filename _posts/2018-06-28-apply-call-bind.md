---
layout: post
title:  "Fuction.prototype.apply, call, bind 차이점"
date:   2018-06-28 17:00:00 +0900
categories: vanillaJS
---

#### Function.prototype.apply
- Syntax
```javascript
function.apply(thisArg, [argsArray])
```
- `thisArg` 를 `this` 객체에 바인딩하고 전달 받은 인자를 `arguments` 에 설정한 후 해당 함수를 호출한다
- `arguments` 를 **배열로** 전달한다
- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply>

<br>

#### Function.prototype.call
- Syntax
```javascript
function.call(thisArg, arg1, arg2, ...)
```
- `thisArg` 를 `this` 객체에 바인딩하고 전달 받은 인자를 `arguments` 에 설정한 후 해당 함수를 호출한다
- `arguments` 를 **순서대로** 전달한다
- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call>

<br>

#### Function.prototype.bind
- Syntax
```javascript
function.bind(thisArg, arg1, arg2, ...)
```
- 첫번째 인자를 this 에 바인딩하고, 두번째 인자부터 arguments 를 **순서대로** 전달한다. 전달된 arguments 를 미리 부분적용한 **함수를 리턴**한다.
- 이후 함수 호출 시 인자를 추가로 전달할 경우 미리 전달받은 arguments 뒤에 concat 된다
- Sample
```javascript
function test(){
    return Object.assign(this, arguments)
};
test = test.bind({}, "a","b","c");
test();  // {0: "a", 1: "b", 2: "c"}
test("z","x","c");  // {0: "a", 1: "b", 2: "c", 3: "z", 4: "x", 5: "c"}
```
- <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind>

