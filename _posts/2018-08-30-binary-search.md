---
layout: post
title: "[알고리즘] 이진 검색"
date: 2018-08-30 15:00
categories:  algorithm
tags: [algorithm, binary-search]
---
#### 문제
<https://www.hackerrank.com/challenges/ctci-ice-cream-parlor/problem>

<br>
#### 풀이
<script src="https://gist.github.com/min9nim/42e33306341c02889a8c33ffe9da0661.js"></script>

<br>
#### 리뷰
- 정렬 후에도 아이스크림의 아이디값 정보를 유지하기 위해 16라인이 반드시? 필요
- binarySearch 함수에서 s가 e 보다 커지는 경우에 대한 예외처리를 하지 않아 무한루프에 빠지면 안됨


