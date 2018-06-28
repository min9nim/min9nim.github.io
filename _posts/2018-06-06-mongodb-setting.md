---
layout: post
title:  "[mongoDB] aws ec2 에서 mongoDB 세팅하기"
date:   2018-06-06 10:00:00 +0900
categories: back-end
---
#### mongodb 설치
1. root 권한으로 전환
```
$ sudo su
```
1. `vi /etc/yum.repos.d/mongodb-org-3.4.repo` 입력 후 아래 내용 저장
```
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```
1. yum 으로 설치
```
$ yum install -y mongodb-org
```

<br>
#### mongodb 서버시작 및 접속
1. 서비스 시작
```
$ sudo service mongod start
```
1. 서비스 재시작
```
$ sudo service mongod restart
```
1. 서버접속
```
$ mongo
```


<br>
#### mongodb 보안 설정
1. 설정을 수정하려면 root 권한이 필요하다.
```
$ sudo vi /etc/mongod.conf
```
1. 외부에서 접근을 허용하려면 `net` 항목의 `bindIp` 항목을 아래와 같이 주석처리한다
```
# network interfaces
net:
  port: 27017
#  bindIp: 127.0.0.1  # Listen to local interface only, comment to listen on all interfaces.
```
1. 익명 로그인을 제한하려면 `security` 항목에 `authorization: enabled` 를 추가한다
```
security:
    authorization: enabled
```


<br>
#### Ref.
- [ec2에 mongoDB설치](https://chichi.space/2017/05/12/한번에-끝내는-AWS-EC2에-MongoDB-설치하고-보안설정하기/)

