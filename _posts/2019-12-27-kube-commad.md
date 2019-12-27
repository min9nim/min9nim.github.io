---
layout: post
title: '[kubernetes] 기본 명령어'
date: 2019-12-27 00:10
categories: kubernetes
tags: [kubernetes, command]
---
기본 명령어들

### 컨테이너 목록 확인
```
kubectl get pod
```

<br>

### 컨테이너 ssh 접속
```
kubectl exec -it xxxxx bash
```

<br>

### kubectl 로그 확인
```
kubectl logs -f xxxxxx
```