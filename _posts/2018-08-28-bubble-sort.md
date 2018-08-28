---
layout: post
title: "[알고리즘] 버블소트"
date: 2018-08-28 01:00:00 +0000
categories: algorithm
tags: [algorithm, bubble-sort]
---
거품정렬은 인접한 두 원소의 크기를 비교하며 배열의 가장 큰(또는 가장 작은) 값을 끝으로 하나씩 밀어낸다. 
마치 거품이 위로 올라가는 듯한 이미지를 연상시키기 때문에 거품정렬이라는 이름이 붙었다.

<br>
### 시간복잡도
O(n^2)

<br>
### 자바스크립트 코드
```javascript
function bubbleSort(a) {
    for(let loop=0; loop < a.length-1; loop++){
        for(let i=0; i < a.length-1-loop; i++ ){
            if(a[i] > a[i+1]){  // 오름차순
                let tmp = a[i];
                a[i] = a[i+1];
                a[i+1] = tmp;
            }
        }
    }
    return a;
}

bubbleSort([1,4,5,2,7,8]);
//  [1, 2, 4, 5, 7, 8]
```


<br>
### Ref.
- <https://ko.wikipedia.org/wiki/거품_정렬>
- <https://www.hackerrank.com/challenges/ctci-bubble-sort/problem>
