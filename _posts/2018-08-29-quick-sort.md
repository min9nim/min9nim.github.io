---
layout: post
title: "[알고리즘] Quick sort"
date: 2018-08-29 01:00:00 +0100
categories: algorithm
tags: [algorithm, quick-sort]
---
퀵소트는 아래와 같은 방법으로 정렬을 진행한다
1. 배열의 요소 중 임의의 값을 pivot 으로 지정
1. pivot 값을 기준으로 pivot보다 작은 값들은 왼쪽에 큰값은 오른쪽으로 정렬한다.
1. 각 왼쪽과 오른쪽 배열에 대해서 요소의 개수가 0 또는 1이 될 때까지 위 1~2 과정을 반복한다

한줄요약
> 임의 값을 기준을 왼쪽/오른쪽 나누고 나뉘어진 상태에 대해서 동일한 작업을 재귀적으로 진행한다.

<br>
### 자바스크립트 코드
```javascript
function quickSort(a){
    if(a.length < 2){
        return a;
    }
    var pivot = a[0];   // 첫번째 요소를 pivot으로 세팅
    var left = [];
    var center = [pivot];
    var right = [];
    for(var i=1; i<a.length; i++){
        if(a[i] > pivot){
            right.push(a[i])
        }else if(a[i] === pivot){
            center.push(pivot);
        }else{
            left.push(a[i]);
        }
    }
    return [...quickSort(left), ...center, ...quickSort(right)];
}

quickSort([7,4,9,8,5,3,2,1,9,3]);
```

위 코드는 이해하기 쉽지만 공간복잡도 O(nLogn) 을 사용한다. 아래와 같이 공간복잡도 O(1)만을 사용하며 퀵소트를 수행하는 것도 가능하다.
(아래 코드는 오류가 있음 수정 필요)
```javascript
function quickSort(a, left=0, right=a.length-1){
    if(right-left < 2){
        return a;
    }
    var pivot = a[left];   // 첫번째 요소를 pivot으로 세팅
    var i = left+1;
    var j = right;
    var tmp;

    while(i < j){
        while(a[i] < pivot) i++;
        while(i<j && a[j] >= pivot) j--;
        tmp = a[i];
        a[i] = a[j];
        a[j] = tmp;
    }
    a[left] = a[i];
    a[i] = pivot;

    console.log("pivot : " + pivot + " > " + a);
    quickSort(a, left, i-1);
    quickSort(a, i+1, right);
}
var arr = [7,4,9,8,5,3,2,1,9,3];
quickSort(arr);
console.log(arr);
```
