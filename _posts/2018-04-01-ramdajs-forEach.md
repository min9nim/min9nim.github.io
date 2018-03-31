---
layout: post
title:  "[ramdajs] forEach 버그"
date:   2018-04-01 00:35:00 +0900
categories: FrontEnd
---
#### 예시
```html
<html>

    <head>
        <script src="//cdn.jsdelivr.net/npm/ramda@0.25/dist/ramda.min.js"></script>
    </head>

    <body>
        <div class="item" />
        <div class="item" />
        <div class="item" />
        <script>
            R.forEach(function() {
                console.log("arguments.length = " + arguments.length)
            }, document.querySelectorAll(".item"));

        </script>
    </body>

</html>
```
<br>

#### 결과
```
arguments.length = 3
```
<br>


#### 질문
[forEach 매뉴얼](http://ramdajs.com/docs/#forEach){:target="_blank"} 을 보면
첫번째 인자 함수가 패러미터를 1개만 받는다고 나와있는데.. 저 경우에는 왜 3개를 받는 걸가?
버그라고 봐야하지 않을까
