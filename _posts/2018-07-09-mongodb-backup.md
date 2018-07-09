---
layout: post
title:  "[mongoDB] 자동 백업"
date:   2018-07-06 16:00:00 +0900
categories: node
---
#### backup.sh 작성
```
#!/bin/sh
mongodump -h 127.0.0.1 -u root -p xxxx -o /home/ec2-user/dbbackup/dump_$(date +%y%m%d-%H%M)
```
<br>

#### crontab 에 등록
```
$ crontab -e
```
입력 후 반복작업 등록
```
# 매시간 정각에 backup.sh 수행
0 * * * * /home/ec2-user/dbbackup/backup.sh
```
<br>

#### 등록된 계획 확인
```
$ crontab -l
# 매시간 정각에 backup.sh 수행
0 * * * * /home/ec2-user/dbbackup/backup.sh
$ 
```
<br>

#### 복구
```
$ mongorestore -h 127.0.0.1 ~/dump/
connected to: 127.0.0.1
....
```
<br>

#### Ref
- [리눅스 크론탭(Linux Crontab) 사용법](https://jdm.kr/blog/2)
- [MongoDB 백업하고 복구하기](https://blog.outsider.ne.kr/790)