---
layout: post
title: "[알고리즘] Quick sort"
date: 2018-08-29 01:00:00 +0100
categories: algorithm
tags: [algorithm, quick-sort]
---
퀵소트는 아래와 같은 방법으로 정렬을 진행한다
1. 배열의 요소 중 임의의 값을 pivot 으로 지정
1. pivot 값을 기준으로 pivot보다 작거나 같은 값들은 왼쪽에 큰값들은 오른쪽에 위치시킨다
1. 각 왼쪽과 오른쪽 배열에 대해서 요소의 개수가 0 또는 1이 될 때까지 위 1~2 과정을 반복한다

한줄요약
> 임의 값을 기준을 왼쪽/오른쪽 나누고 나뉘어진 상태에 대해서 동일한 작업을 재귀적으로 진행한다.

<br>
### 특징
- 분할&정복
- 불안정정렬
-  O(nLogn)

<br>
### js 코드
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
/*
[1, 2, 3, 3, 4, 5, 7, 8, 9, 9]
*/
```

<br>
위 코드는 이해하기 쉽지만 공간복잡도 O(nLogn) 을 사용한다. 아래와 같이 공간복잡도 O(1)를 사용하는 구현도 가능하다. 하지만 코드의 디테일을 정확히 이해하기가 만만치 않다.
```javascript
function swap(arr, i1, i2){
    var tmp = arr[i1];
    arr[i1] = arr[i2];
    arr[i2] = tmp;
}

function log(pivot, left, right, a){
    var head = "x".repeat(left).split("");
    var body = a.slice(left, right+1);
    var tail = "x".repeat(a.length-1-right).split("");
    console.log("p(" + pivot + ") => " + [...head, ...body, ...tail]);    
}

function quickSort(a, left=0, right=a.length-1){
    if(left >= right){
        return;
    }
    var pivot = a[left];   // 첫번째 요소를 pivot으로 세팅
    var i = left;
    var j = right;

    while(i < j){
        while(pivot < a[j]) j--;    // 오른쪽끝부터 왼쪽으로 pivot 보다 작거나 같은 값의 위치를 찾는다
        while(i<j && a[i] <= pivot) i++;    // 왼쪽끝부터 오른쪽으로 pivot보다 큰값의 위치를 찾는다
        swap(a, i, j);      // 두 값을 교환
    }
    swap(a, left, i);   // swap 결과 i 위치를 기준으로 왼쪽은 모두 pivot 보다 작거나 같은 값이 되고, 오른쪽은 pivot보다 큰 값이 위치하게 된다

    log(pivot, left, right, a); // pivot 으로 양분된 결과 출력

    quickSort(a, left, i-1);
    quickSort(a, i+1, right);
}
var arr = [4,5,7,5,4,2,6,0,8,3,1,3,9];
quickSort(arr);
console.log(arr);
/*
p(4) => 0,3,1,3,4,2,4,6,8,5,7,5,9
p(0) => 0,3,1,3,4,2,x,x,x,x,x,x,x
p(3) => x,2,1,3,3,4,x,x,x,x,x,x,x
p(2) => x,1,2,3,x,x,x,x,x,x,x,x,x
p(6) => x,x,x,x,x,x,x,5,5,6,7,8,9
p(5) => x,x,x,x,x,x,x,5,5,x,x,x,x
p(7) => x,x,x,x,x,x,x,x,x,x,7,8,9
p(8) => x,x,x,x,x,x,x,x,x,x,x,8,9
[0, 1, 2, 3, 3, 4, 4, 5, 5, 6, 7, 8, 9]
*/
```
