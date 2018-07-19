---
layout: post
title:  "[vanillaJS] 활용 팁"
date:   2018-07-06 16:00:00 +0900
categories: vanillaJS
---
#### 배열의 마지막 요소 참조
배열의 마지막 요소를 아래와 같이 인덱스 참조로 접근할 수 있지만, 
```javascript
let arr = [1,2,3];
arr[arr.length-1]
```
배열이 특정 객체의 속성으로 depth 가 깊어지면 아무래도 불편하다. 
```javascript
tech.user.post.comment = ["a", "b", "c"];
tech.user.post.comment[tech.user.post.comment.length-1]
```

좀더 깔끔한 표현을 찾아보았다. (es5 방식이 좀 더 보기 좋은거 같다)
```javascript
// es5
let arr = [1,2,3];
arr.slice().pop();

// es6
let arr = [1,2,3];
[...arr].pop();
```


