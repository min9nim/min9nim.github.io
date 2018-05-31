---
layout: post
title:  "git 명령어 요약"
date:   2018-04-01 01:14:00 +0900
categories: FrontEnd
---
### 브랜치
* 브랜치 생성
```
$ git branch iss53
```
* 브랜치 이동
```
$ git checkout iss53
```
* 브랜치 목록 보기
```console
$ git branch
  iss53
> master
  testing
```
* 브랜치를 만들면서 Checkout까지 한 번에
```
$ git checkout -b iss53
```
위 명령은 아래 명령을 줄여놓은 것
```
$ git branch iss53
$ git checkout iss53
```
* master 브랜치에서 hotfix 브랜치를 merge 하고자 한다면
```
$ git checkout master
$ git merge hotfix
```
* merge 된 브랜치 목록
```
$ git branch --merged
```
* 아직 merge 안 된 브랜치 목록
```
$ git branch --no-merged
```
* iss53 브랜치를 삭제
```
$ git branch -d iss53
```
<br>

### 로그
* commit 메세지만 한줄로 & 그래프로 보이기
```
$ git log --oneline --graph
```
* commit 의 diff 결과를 최근 2개만 보이기
```
$ git log -p -2
```
<br>

### 기타
* workingDirectory & staging 영역에서 파일 삭제
```
$ git rm test.html
```
* 저장소 내려받기  
(명령을 수행하는 경로에 min9nim.github.io 폴더를 만들고 그 아래에 소스를 내려받음)
```
$ git clone https://github.com/min9nim/min9nim.github.io.git
```
<br>


### Ref.
* <https://git-scm.com/book/ko/v2/Git-브랜치-브랜치와-Merge-의-기초>
* <https://git-scm.com/book/ko/v1/Git의-기초-커밋-히스토리-조회하기>
* <https://backlog.com/git-tutorial/kr/stepup/stepup1_1.html>
