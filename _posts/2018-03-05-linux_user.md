---
title: "리눅스 계정관리 명렁어"
categories: posts
tags:
  - etc
date: 2018-03-05 00:00:00 -0400
---


## 계정관리 명령어


### [사용자 계정추가]
```
# useradd 사용자명
```


### [계정확인]
```
# /etc/passwd | grep 사용자명
```


### [useradd 명령어를 사용해서 사용자 계정을 추가할 때 기본 적용되는 정보]
```
GROUP : 기본 그룹 ID  // = 100

HOME  : 홈 디렉토리 경로  // = /home

INACTIVE : 암호만료 후 사용가능한 기간 지정  // = -1

EXPIRE : 만료일 지정

SHELL : 기본 쉘   // = /bin/bash

SKEL : 기본 환경 설정 파일이 존재하는 디렉토리  // = /etc/skel

CREATE_MAIL_SPOOL : 계정의 메일 저장 파일 생성 유무 // = yes
```


### [useradd (옵션) 명령어]
```
b : 루트 밑의 홈 디렉토리 밑에 계정까지만

d : 홈 디렉토리 설정

g : 그룹아이디 지정

G : 2차 그룹 GID 지정
```



### [사용자계정 암호설정확인]
```
# /etc/shadow
```


### [사용자 계정 암호설정하기]
```
# passwd 사용자명

Changing passwd for user 사용자명

New UNIX password: 새로운 암호

Retype new UNIX password: '새로운 암호' 재확인
```


### [사용자계정설정변경]
```
# usermod
```


### [현재의 comment 확인]
```
etc/passwd | grep 사용자명
```


### [comment변경하기]
```
# usermod -c 문구(testaccount) 사용자명
```


### [홈 디렉토리 변경]
```
# usermod -d
```


### [홈 디렉토리 만들기]
```
# mkdir /home/디렉토리명
```


### [홈 디렉토리 변경]
```
# usermod -d /home/디렉토리명 사용자명
```


### [사용자 계정 삭제하기]
```
# userdel 사용자명  // (이 처럼 아무옵션 없이 삭제하면 홈디렉토리(/home/디렉토리) 는 삭제되지 않는다.)
```


### [홈디렉토리 유저 삭제]
```
# rm -rf /home/디렉토리명  // userdel -r 사용자명 -r 옵션 사용시  rm -rf 와 같다. 
```


### [그룹의 기본정보 확인]
```
# /etc/group
```


### [그룹 패스워드 정보]
```
# /etc/gshadow
```


### [그룹지정 변경]
```
# usermod[옵션] 계정명  // 옵션은 useradd옵션과 거의 동일
```


### [그룹생성]
```
# groupadd[옵션] 그룹명

g : GID지정 옵션

o : 중복 GID지정시 사용 옵션

r : 0~499번까지 자동 지정 옵션
```


### [그룹삭제]
```
# groupdel 그룹명
```


### [그룹수정]
```
# groupmod[옵션] 그룹명

g : GID 지정 옵션

n : 그룹명 변경 옵션
```


### [그룹암호변경]
```
# gpasswd[옵션] 그룹명

A : 관리자 추가 옵션

a : 구성원 추가 옵션

d : 구성원 제거 옵션

M : 구성원 변경 옵션
```

