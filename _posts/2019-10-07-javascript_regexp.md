---
title: "[JavaScript] 자주 사용하는 정규식 메모"
categories: posts
tags:
  - JavaScript
date: 2019-10-07 00:00:00 -0400
---


### 자주 쓰는 정규식 메모

 
```
//숫자 3단위마다 콤마 찍기

var numberWithCommas= function(num){

  return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");

}

// 아이디 체크 정규식
const regExpId = /^[a-z0-9_-]\w{5,20}$/;
  
// 비밀번호 길이 체크 정규식
const regExpPassword = /^\w[6,16]$/;
  
// 비밀번호 조합(영문, 숫자) 및 길이 체크 정규식
const regExpPassword = /^(?=.*[a-zA-Z])(?=.*[0-9]).{6,16}$/;
  
// 이메일 체크 정규식
const regExpEmail=/^([\w-]+(?:\.[\w-]+)*)@((?:[\w-]+\.)*\w[\w-]{0,66})\.([a-z]{2,6}(?:\.[a-z]{2})?)$/;
  
// 휴대폰번호 정규식
const regExpMobile = /^01([016789]?)-?([0-9]{3,4})-?([0-9]{4})$/;
  
// 숫자만 사용 정규식
const regExpNumber = /^\d+$/;
```

