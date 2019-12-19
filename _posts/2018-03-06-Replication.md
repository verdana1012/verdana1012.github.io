---
title: "Replication"
categories: posts
tags:
  - etc
date: 2018-03-06 00:00:00 -0400
---


## Replication

데이터를 물리적으로 다른 서버의 저장공간에 동일한 데이터를 복사하는것.  
1개의 마스터와 n개의 슬레이브로 구성.   
마스터에서만 데이터변경(읽기포함) 작업 수행이 가능하며 슬레이브에서는 읽기작업만 가능.  

Replication 기능과 용도는 각각의 데이터 베이스 특징에 따라 다르지만   
기본적으로 데이터 백업과 복구를 의미하 는 것은 같다.   
Mysql 에서 Replication 은 백업/복구는 물론 미러링 구축으로 활용하기 좋은 도구이다.   
또한 마스터 서버의 데이터 베이스에 과부하가 걸리는 경우, Replication   
을 통해 슬레이브 서버로의 효과적인 분산이 가능하다.   


### 장점
 과부하 마스터서버의 부하 분산서버로 활용 ,  
 마스터에서 장애발생시 슬레이브를 이용하여 자료의 유실없이 마스터 복구 가능  

### 단점
 바이너리 로그 관리 - 마스터에 쌓이는 바이너리 로그를 수동으로 처리해야한다. (크론 등을 이용해서 정기적인 삭제필요)  
 마스터의 처리량이 많은경우 슬레이브의 지연시간 발생으로 데이터가 동일하지 않는 경우가 생길수도있다.  



## [Mysql Replication 의 특징]

대략적인 기능상의 특징은 다음과 같다.   

- 마스터-> 슬레이브로의 일방향 복제기능  
- 바이너리 로그(binlog)를 이용한 미러링  
- 쿼리에 의한 부하 분산  
- 다수의 슬레이브 서버를 이용한 부하 분산  



## [REPLICATION 작동 원리]

마스터와 슬레이브의 Mysql 데이터베이스를 같은 환경(매우 중요)으로 설치하여   
마스터 서버와 슬레이브 서버에 각각 Mysql 서버 고유넘버를 지정한다.   
마스터와 슬레이브는 이 고유넘버 로 서로를 인식하여 작동하게 된다.   

Mysql Replication 은 마스터에 입력되는 쿼리를 바이너리 로그에 기록하게 되고,   
슬레이브는 마스터의 바이너리 로그의 업데이트 여부를 추적하여   
업데이트 된 경우, 바이너리 로그에 기록된 쿼리문을 슬레이브로 가져와 처리하게 된다.   
<ins>(설치과정시 mysql-bin 로그가 쌓일 수 있도록 설정해줘야 하고, slave에서 master 의 mysql-bin 로그를 참조해 동기화를 시킨다.)</ins>  
즉 실시간 미러링이 되며 마스터와 동일한 자료를 보유하게 된다.   
만일 이 과정에서 에러가 발생하는 경우, 슬레이브는 에러 로그를 작성한다.   



## [REPLICATION 이 지원하지 않는 것]

현재 Mysql Replication 은 쿼리 단위로의 미러링을 지원한다.   
이에 따른 중요 문제가 발생한다.   

> RAND() in updates does not replicate properly. 
> Use RAND (some_non_rand_expr) if you are replicating updates with RAND(). 
> You can, for example, use UNIX_TIMESTAMP() for the argument to RAND()


랜덤 함수에 의해 발생되어지는 자료에 대한 업데이트가 이루어지지 않는다.   
랜덤 함수가 발생한 필드의 자료는 공란(null)로 입력된다.   

> LOAD DATA INFILE will be handled properly as long as the file 
> still resides on the master server at the time of update propagation. 
> LOAD LOCAL DATA INFILE will be skipped. 


load data infile 에 의한 데이터 입력시 마스터 서버에 파일이 남아 있는 상태에서만 가능하다.   
이와는 반대로 load local data infile 은 업데이트 되지 않는다.   



## [REPLICATION 활용 방안]

### 미러링으로 활용 

마스터의 Mysql data를 실시간으로 백업 받는다.   
마스터 서버에 장애가 발생하여 미러링 서버가 작동하게 되면 자연적으로   
슬레이브 Mysql 이 작동하게 되며, 마스터 복구시 init.sh 를 통해 슬레이브의 데이터를 받아오므로   
거의 자료의 유실 없이 Mysql 서버를 복구할수 있다.   


### 과부하 마스터서버의 부하 분산서버로 활용 

Mysql 에 과부하를 유발하는 마스터서버의 슬레이브를 설정하여 쿼리문을 분산시킨다.   
즉 마스터서버에서는 데이터 전송이 적은 UPDATE, INSERT, DELETE 문을 사용하고   
슬레이브서버에서는 데이터 전송이 많은 SELECT 문을 사용하도록한다.   

