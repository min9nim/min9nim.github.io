---
layout: post
title:  "[js] 객체와 prototype 의 이해"
date:   2018-05-04 13:00:00 +0900
categories: frontend
---

Intro
---
* 자바스크립트는 prototype 을 이용해 완전하지는 않지만 그럴듯하게 객체지향프로그래밍을 흉내낼 수 있다. 기존 자바의 클래스 기반 객체생성 및 상속에 익숙해져 있는 사람이라면 자바스크립트의 객체 생성 및 상속의 개념이 상당히 이질적으로 느껴질 수 있다. 자바스크립트로 객체지향프로그래밍을 하고자 한다면 prototype 에 대한 정확한 이해는 무엇보다 중요하다.
* 이 글은 자바스크립트를 처음 접하는 사람들에게 친절하지 않다. 반면 prototype의 동작방식을 대충은 알지만 정확하게 알지 못한 채 자바스크립트를 습관적으로 사용하던 개발자에게 prototype 의 정확한 이해를 돕는데 집중한다.

<br/>

자바스크립트의 객체
---
* 자바스크립트의 primitive 데이터타입 5가지
  * 숫자, 문자열, 불리언(true/false), null, undefined
  * 숫자/문자열/불리언은 메소드를 가지고 있기 때문에 객체처럼 보일 수 있지만 일반적인 객체와 달리 이 값들은 한번 정해지면 변경이 불가합니다(immutable)
  * primitive 타입을 제외한 모든 값은 객체
* 자바스크립트에서 객체란 변경 가능한 속성들의 집합
  * ex) 배열, 함수, 정규표현식
  * 속성의 이름은 문자열이면 모두 가능, 빈문자열도 허용
  * 속성의 값으로는 자바스크립트의 모든 값이 가능
    * [The Good Parts
by Douglas Crockford][1] 에서는 undefined 는 속성의 값으로 사용할 수 없다고 되어있는데 책집필 당시에서 그랬었는지 모르겠지만 최근에는 undefined 도 속성의 값으로 들어가는 것으로 확인됩니다
  * 자바스크립트의 객체는 클래스가 불필요
  * 자바스크립트는 특정 객체에 있는 속성들을 다른 객체에 그대로 상속하게 해주는 간단한 방법을 제공하는데 그것이 바로 prototype 연결
  * 객체는 참조방식으로 전달, 결코 복사되지 않음
  * 객체리터럴로 생성되는 모든 객체는 Object.prototype 객체에 연결됨
  * 객체를 생성할 때는 해당 객체의 프로토타입이 될 객체를 선택할 수 있음


<br>
 
객체 생성 방법 
---
prototype 을 선택하여 객체를 생성하는 방법은 2가지가 있다
1. new 연산자를 이용하는 방법
  * 생성자 함수를 정의하고 new 연산자와 함께 생성자 함수를 호출하면 생성자함수의 prototype에 연결을 갖는 새로운 객체가 생성되고 생성자 함수에 의해 새로운 객체의 속성이 초기화 된다
  <script src="https://gist.github.com/min9nim/7a384c89b085ac41ab72f53e0b5c19fb.js"></script>
  * new 연산자의 동작을 Function의 메소드로 정의 한다면 아래와 같을 것이다
  <script src="https://gist.github.com/min9nim/72fd726a2ff9f6b8d61ad8c534a4a756.js"></script>


1. Object.create 를 이용하는 방법
  * prototype으로 사용할 객체를 인자로 전달하면 해당 객체가 prototype으로 연결된 새로운 객체가 생성된다
  <script src="https://gist.github.com/min9nim/5cf5cd11463c79bc3de2f9039c8b2e76.js"></script>
  * Object.create 가 지원되지 않는다면 아래와 같이 간단하게 polyfill 을 구현할 수 있다.
  <script src="https://gist.github.com/min9nim/02f40a241014c6f13e0337cac84cb9f0.js"></script>

1. 위 두가지 방식의 유일한 차이점은 1번방식으로 생성된 객체는 해당 속성들이 열거 가능하지만, 2번방법으로 생성된 속성들은 열거 가능하지 않다는 점이다
  * 1번 방법으로 생성된 객체
  <script src="https://gist.github.com/min9nim/a6ab5bd9563bca5dd35671f64b67a258.js"></script>
  * 2번 방법으로 생성된 객체
  <script src="https://gist.github.com/min9nim/6eb131fd72ec002edfa075e7e2154aea.js"></script>




<br/>


Ref.
---
<https://7chan.org/pr/src/OReilly_JavaScript_The_Good_Parts_May_2008.pdf>
<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/create>



[1]: https://7chan.org/pr/src/OReilly_JavaScript_The_Good_Parts_May_2008.pdf

