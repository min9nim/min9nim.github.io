---
layout: post
title:  "ramdajs 주요 함수"
date:   2018-06-28 01:00:00 +0900
categories: ramdajs
---
흔히 사용될 수 있는 ramdajs 함수들을 알아본다
<br>
<br>
#### R.append
배열의 끝에 특정 요소를 추가한다. Array.prototype.push 와 유사
```javascript
R.append('tests', ['write', 'more']); //=> ['write', 'more', 'tests']
```
vanillaJS 예제)
```javascript
const arr = ['write', 'more'];
arr.splice(arr.length, 0, "tests");
console.log(arr);           //  ['write', 'more', 'tests']
```
<br>

#### R.prepend
배열의 처음에 특정 요소를 추가
```javascript
R.prepend('fee', ['fi', 'fo', 'fum']); //=> ['fee', 'fi', 'fo', 'fum']
```
vanillaJS 예제)
```javascript
const arr = ['fi', 'fo', 'fum'];
arr.splice(0,0,"fee");      // []  cause) 제거된 요소들이 없으므로
console.log(arr);           // ["fee", "fi", "fo", "fum"]
```
<br>

#### R.insert
배열의 특정 위치에 요소를 삽입, Array.prototype.splice 와 유사
```javascript
R.insert(2, 'x', [1,2,3,4]); //=> [1,2,'x',3,4]
```
vanillaJS 예제)
```javascript
const arr = [1,2,3,4];
arr.splice(2,0,"x");
console.log(arr);           // [1,2,'x',3,4]
```

<br>

#### R.pipe
순서대로 연결된 함수를 리턴
```javascript
var f = R.pipe(Math.pow, R.negate, R.inc);
f(3, 4); // -(3^4) + 1
```
<br>

#### R.compose
역순으로 연결된 함수를 리턴
```javascript
R.compose(Math.abs, R.add(1), R.multiply(2))(-4);
// => 7  cause) | (-4 * 2) + 1 |
```
<br>

#### R.flip
첫번째 두번째 인자의 위치 순서를 뒤집어 놓은 함수를 리턴
```javascript
var mergeThree = (a, b, c) => [].concat(a, b, c);
mergeThree(1, 2, 3); //=> [1, 2, 3]
R.flip(mergeThree)(1, 2, 3); //=> [2, 1, 3]
```
<br>

#### R.forEach
배열의 각 요소를 인자로 전달받는 특정 함수를 실행시키고 인자로 전달받았던 배열을 리턴한다
- Array.prototype.forEach 는 undefined 를 리턴

```javascript
var printXPlusFive = x => console.log(x + 5);
R.forEach(printXPlusFive, [1, 2, 3]); //=> [1, 2, 3]
// logs 6
// logs 7
// logs 8
```
<br>

#### R.map
리스트의 각 요소를 다른 값으로 매핑한다. Array.prototype.map 와 유사
```javascript
var double = x => x * 2;
R.map(double, [1, 2, 3]); //=> [2, 4, 6]
R.map(double, {x: 1, y: 2, z: 3}); //=> {x: 2, y: 4, z: 6}
```
<br>

#### R.filter
배열의 특정 요소들만 필터링.  Array.prototype.filter 와 유사
```javascript
var isEven = n => n % 2 === 0;
R.filter(isEven, [1, 2, 3, 4]); //=> [2, 4]
R.filter(isEven, {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, d: 4}
```
<br>

#### R.reduce
리스트의 각 요소를 순회하며 특정 값으로 축약한다/ Array.prototype.reduce 와 유사
```javascript
R.reduce(R.subtract, 0, [1, 2, 3, 4]) // => ((((0 - 1) - 2) - 3) - 4) = -10
//          -               -10
//         / \              / \
//        -   4           -6   4
//       / \              / \
//      -   3   ==>     -3   3
//     / \              / \
//    -   2           -1   2
//   / \              / \
//  0   1            0   1
```
<br>


#### R.prop
객체의 특정 속성의 값을 리턴한다
```javascript
R.prop('x', {x: 100}); //=> 100
R.prop('x', {}); //=> undefined
```
<br>

#### R.props
여러개의 속성의 값을 배열로 리턴
```javascript
R.props(['x', 'y'], {x: 1, y: 2}); //=> [1, 2]
R.props(['c', 'a', 'b'], {b: 2, a: 1}); //=> [undefined, 1, 2]

var fullName = R.compose(R.join(' '), R.props(['first', 'last']));
fullName({last: 'Bullet-Tooth', age: 33, first: 'Tony'}); //=> 'Tony Bullet-Tooth'
```
<br>

#### R.find
배열에서 특정 조건을 만족하는 첫번재 요소를 리턴. Array.prototype.find 와 유사
```javascript
var xs = [{a: 1}, {a: 2}, {a: 3}];
R.find(R.propEq('a', 2))(xs); //=> {a: 2}
R.find(R.propEq('a', 4))(xs); //=> undefined
```
vanillaJS
```javascript
var xs = [{a: 1}, {a: 2}, {a: 3}];
xs.find(o => o.a === 2); //=> {a: 2}
xs.find(o => o.a === 4); //=> undefined
```
<br>

#### R.findIndex
배열에서 특정 조건을 만족하는 첫번째 요소의 인덱스를 리턴. Array.prototype.findIndex 와 유사
```
var xs = [{a: 1}, {a: 2}, {a: 3}];
R.findIndex(R.propEq('a', 2))(xs); //=> 1
R.findIndex(R.propEq('a', 4))(xs); //=> -1
```
<br>

#### R.propEq
속성의 값이 특정 값과 일치하는지 여부를 리턴
```javascript
var abby = {name: 'Abby', age: 7, hair: 'blond'};
var fred = {name: 'Fred', age: 12, hair: 'brown'};
var rusty = {name: 'Rusty', age: 10, hair: 'brown'};
var alois = {name: 'Alois', age: 15, disposition: 'surly'};
var kids = [abby, fred, rusty, alois];
var hasBrownHair = R.propEq('hair', 'brown');
R.filter(hasBrownHair, kids); //=> [fred, rusty]
```
<br>

#### R.propIs
속성의 값의 타입이 특정 타입과 일치하는지 여부를 리턴
```javascript
R.propIs(Number, 'x', {x: 1, y: 2});  //=> true
R.propIs(Number, 'x', {x: 'foo'});    //=> false
R.propIs(Number, 'x', {});            //=> false
```
<br>

#### R.range
특정 범위의 연속적인 자연수 배열을 리턴
```javascript
R.range(1, 5);    //=> [1, 2, 3, 4]
R.range(50, 53);  //=> [50, 51, 52]
```
<br>

#### R.add
두 수의 합을 리턴
```javascript
R.range(1, 5);    //=> [1, 2, 3, 4]
R.range(50, 53);  //=> [50, 51, 52]
```
<br>

#### R.and
두 값의 && 연산 결과를 리턴
```javascript
R.and(true, true); //=> true
R.and(true, false); //=> false
R.and(false, true); //=> false
R.and(false, false); //=> false
```
<br>

#### R.or
두 값의 || 연산 결과를 리턴
```javascript
R.or(true, true); //=> true
R.or(true, false); //=> true
R.or(false, true); //=> true
R.or(false, false); //=> false
```
<br>

#### R.partial
왼쪽부터 인자가 부분적용된 함수를 리턴
```javascript
var multiply2 = (a, b) => a * b;
var double = R.partial(multiply2, [2]);
double(2); //=> 4

var greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

var sayHello = R.partial(greet, ['Hello']);
var sayHelloToMs = R.partial(sayHello, ['Ms.']);
sayHelloToMs('Jane', 'Jones'); //=> 'Hello, Ms. Jane Jones!'
```
<br>

#### R.partialRight
오른쪽부터 인자가 부분적용된 함수를 리턴
```javascript
var greet = (salutation, title, firstName, lastName) =>
  salutation + ', ' + title + ' ' + firstName + ' ' + lastName + '!';

var greetMsJaneJones = R.partialRight(greet, ['Ms.', 'Jane', 'Jones']);

greetMsJaneJones('Hello'); //=> 'Hello, Ms. Jane Jones!'
```
<br>

#### R.partition
특정 기준으로 리스트를 둘로 나눔
```javascript
R.partition(R.contains('s'), ['sss', 'ttt', 'foo', 'bars']);
// => [ [ 'sss', 'bars' ],  [ 'ttt', 'foo' ] ]

R.partition(R.contains('s'), { a: 'sss', b: 'ttt', foo: 'bars' });
// => [ { a: 'sss', foo: 'bars' }, { b: 'ttt' }  ]
```
<br>

#### R.equals
두 값을 비교, 순환참조 객체도 비교 가능
```javascript
R.equals(1, 1); //=> true
R.equals(1, '1'); //=> false
R.equals([1, 2, 3], [1, 2, 3]); //=> true

var a = {}; a.v = a;
var b = {}; b.v = b;
R.equals(a, b); //=> true
```
<br>

#### R.contains
리스트에 특정 요소가 포함되는지 여부를 리턴. 내부적으로 R.equals 를 이용해 비교
```javascript
R.contains(3, [1, 2, 3]); //=> true
R.contains(4, [1, 2, 3]); //=> false
R.contains({ name: 'Fred' }, [{ name: 'Fred' }]); //=> true
R.contains([42], [[42]]); //=> true
```
<br>

#### R.any
리스트에서 특정 조건을 만족하는 요소가 있는지 여부를 리턴
```javascript
var lessThan0 = R.flip(R.lt)(0);
var lessThan2 = R.flip(R.lt)(2);
R.any(lessThan0)([1, 2]); //=> false
R.any(lessThan2)([1, 2]); //=> true
```
<br>

#### R.tail
머리 빼고 리턴
```javascript
R.tail([1, 2, 3]);  //=> [2, 3]
R.tail([1, 2]);     //=> [2]
R.tail([1]);        //=> []
R.tail([]);         //=> []

R.tail('abc');  //=> 'bc'
R.tail('ab');   //=> 'b'
R.tail('a');    //=> ''
R.tail('');     //=> ''
```
<br>

#### R.split
문자열을 특정 기준으로 나눔,  String.prototype.split 과 유사
```javascript
var pathComponents = R.split('/');
R.tail(pathComponents('/usr/local/bin/node')); //=> ['usr', 'local', 'bin', 'node']
R.split('.', 'a.b.c.xyz.d'); //=> ['a', 'b', 'c', 'xyz', 'd']
```
<br>
