---
title: "3 way hand shake"
categories: posts
tags:
  - etc
date: 2018-03-02 00:00:00 -0400
---


## 3 way hand shake

TCP(Transmission Control Protocol) 네트워크의 정보전달을 통제하는 프로토콜로서,  
흐름제어와 오류제어 기능을 제공하며 신뢰성 있는 연결지향 통신 방식.  

**TCP 고유의 연결방식 이다.**

통신을 시작하기에 앞서 세번의 확인작업을 거치게 되는데 이를 3-Way hand shake 라고 한다.  
3-way hand shake를 통하여 TCP가 신뢰성 연결지향 방식이 될 수 있다.  


### [작동 방식]

1. Client가 Server에게 동기화 요청(SYN)한다.  
2. Server가 Client의 요청을 받아들이겠다고 대답하고(ACK), 똑같이 Client에게 동기화 요청(SYN)을 한다.  
3. Client가 Server의 동기화 요청을 응답(ACK)해주면서 Client와 Server 사이에 세션이 이루어지게 된다.  


* * *

**1. SYN Segment (Client의 Synchronization Information 전송)**

Client는 Source Port에 자신을 나타내는 Port Number를 넣고,   
Destination Port에는 Server를 가리키는 Port Number를 넣는다.   
Sequence Number에 Client의 ISN(Initialization Sequence Number)를 넣고,   
Acknowledgment Number는 0을 넣고, Flag는 SYN bit를 1로 설정하여 전송한다.  

* * *

**2. SYN+ACK Segment (Server의 Synchronization Information 전송 + SYN Segment 수신 확인)**

Server는 Source Port에 자신의 Port Number를 넣고, Destination Port에는 Sender의 Port Number를 넣는다.   
Sequence Number에는Server의 ISN를 넣고, Acknowledgment Number에는 “Client의 ISN + 1”의 값을 넣고,   
Flag는 SYN 와 ACK bit를 모두 1로 설정하여 전송한다.  

* * *

**3. ACK Segment (SYN Segment 수신 확인)**

Client는  첫번째 단계와 동일하게 Source Port와 Destination Port를 설정하고,  
Acknowledgment Number에는 “Server의 ISN + 1”의 값을 넣고, Flag는 ACK bit를 1로 설정하여 전송한다.  

* * *

### [문제점]

서로 보낸 Seq, Ack 번호가 다를 경우 뭔가 잘못되었기 때문에 통신이 이루어지지 않는다.  
client가 1번만 보내고 대기하게 되면 서버는 몇 초간 대기한다.  
엄청나게 많은 1번이 오면 서버가 멈춘다. (AF_RAW 옵션으로 ip spoofing으로 DOS 공격이 이런 경우이다.)

