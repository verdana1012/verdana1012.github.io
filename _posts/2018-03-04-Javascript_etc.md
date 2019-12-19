---
title: "[JavaScript] 나쁘지만 사용해야 하는 부분"
categories: posts
tags:
  - JavaScript
date: 2018-03-04 00:00:00 -0400
---


## 나쁘지만 사용해야 하는 부분
- 자바스크립트에서 나쁘지만 피하기 힘든 문제가 있는 부분들을 잘 인지하여 사용할 수 있도록 하자.   



### 전역변수

- 전역변수는 모든 유효범위(scope) 에서 접근할 수 있는 변수.   
- 전역변수를 잦게 사용하면 플러그인 충돌, 다른 영역에서 다른 목적으로    
동일한 전역변수를 정의할 경우 덮어쓰게 되는 점 등의 오류가 발생하고 어디가 잘못되었는지 찾기 힘들다.   
- 전역변수의 생성은 세가지가 있다.   


1) 어떠한 함수에도 속하지 않은 위치에서 (함수 밖에서) var 문으로 선언   

```
var test = 'test';
```


2) 전역객체에 직접적으로 속성을 추가.   

```
window.test = 'test';
```


3) var 없이 변수를 선언 (함수 내에서도 var 없이 선언하면 전역변수가 된다)   

```
test = 'test';
```


이러한 방법들은 초보자들이 변수를 선언하지 않아도 사용할 수 있게 하기 위해서 고안된 부분들이다.




### 유효범위

- 대부분의 언어에서는 일반적으로 변수가 처음 사용되는 지점에서 변수를 선언하는 것이 좋지만,   
  자바스크립트에서는 모든 변수는 함수의 맨 위에 선언하는것이 좋다.   
  이로인해 변수 초기화의 실수를 최소화 할 수 있고, minification에 유리하다.   
- 자바스크립트의 minification이란 소스의 사이즈를 줄여서 다른사람이 사용할 때의   
  소스의 크기를 최대한 줄여서 성능 최적화를 할 수 있는 프로세스다.   
  이때 var 변수를 산단에 정의해둔 소스파일이 압축율이 훨씬 더 좋기때문에   
  변수선언의 위치는 항상 습관을 들여두도록 하자.   



### 세미콜론 삽입

- 세미콜론의 삽입 위치에 따라 프로그램이 잘못 해석하게 되는 경우가 있다.   

```
// 예) return 문으로 값을 반환할때의 세미콜론은 반드시 return문과 같은 줄에 있어야 한다.

var test = function(){
    return {
        test_return: true
    };
}

console.log( test() );   // <-- Object{ test_return: true } 출력
var test = function(){
    return    // <-- return 문 한줄로 반환이 끝난걸로 인식한다.
    {
        test_return: true
    };
}

console.log( test() );   // undefined 출력
```



### `+` 연산자

- `-` `+` 연산자는 숫자타입의 덧셈을 하거나 문자열을 연결한다.   
- 연산하는 값 중 문자열이 하나라도 포함되어있으면 나머지 숫자형의 값도 문자열로 변환하여 결과값을 돌려준다.   
- `+` 연산자를 더하기로 사용한다면 반드시 숫자형인지 먼저 체크를 해주어야한다.   



### 거짓인 값들

- 자바스크립트의 null, ''(빈문자열), false, NaN(숫자가 아님), undefined 이러한 값들은 거짓인 값 들이다.   
  그 중 NaN 과 undefined 는 상수가 아니다. 이 둘은 전역변수여서 원하는 경우에는 값을 변경하는것이 가능하다.   
  실제로 변경이 불가능 해야하는것이 맞으므로 절대 undefined와 NaN의 값을 변경해서는 안된다.   



## 나쁜점들

- 자바스크립트에서 사용할 경우 문제가 될 수 있는 부분이며  사용하지 않을수록 좋고, 쉽게 피할수 있는 부분들이다.   



### 비교연산자

- 자바스크립트는 비교 연산자로 === / !== 가 있지만, 나쁜 방식으로 == / != 도 존재한다.    

```
if( '' == '0' ? console.log('true') : console.log('false') );          // <-- false 출력
if( 0 == '' ? console.log('true') : console.log('false') )             // <-- true 출력
if( 0 == '0' ? console.log('true') : console.log('false') )            // <-- true 출력

if( false == 'false' ? console.log('true') : console.log('false') )    // <-- false 출력
if( false == '0' ? console.log('true') : console.log('false') )        // <-- true 출력

if( false == undefined ? console.log('true') : console.log('false') )  // <-- false 출력
if( false == null ? console.log('true') : console.log('false') )       // <-- false 출력
if( null == undefined ? console.log('true') : console.log('false') )   // <-- true 출력
```

- 위에있는것은 === 연산자를 사용하면 모두 거짓이다.   
이처럼 서로 다른 값인데도 비교연산자를 통해 true 로 나올 경우가 있으므로 반드시 == / != 는 사용하지 않도록 한다.   



### eval 함수

- eval 함수는 문자열을 자바스크립트 컴파일러에 넘긴 후 결과를 실행시키는 함수이다.   

```
var dateFn = "Date(2017,12,25)";
var myDate;

eval("myDate = new " + dateFn + ";");

console.log('eval을 사용 : ' + myDate);   // <-- Thu Jan 25 2018 00:00:00 GMT +0900 (대한민국 표준시)

myDate2 = new Date(2017,12,25);
console.log('eval 미사용 : ' + myDate2);  // <-- Thu Jan 25 2018 00:00:00 GMT +0900 (대한민국 표준시)
```

- eval을 사용한 코드는 읽기도 매우 어렵고, 단순한 할당문 실행을 위하여 컴파일러를 기동해야 하므로 속도저하가 생긴다.   
- eval은 대부분 자바스크립트에 대한 온전한 이해가 없는 사람들이 가장 많이 사용한다.   
  자바스크립트 에서는 대부분의 경우가 eval함수를 사용하지 않고서도    
  충분히 동일한 동작을 구현할 수 있는 경우가 많으므로 eval함수의 사용은 권장되지 않는다.   



### 블록이 없는 문장

- if/while/do/for 문은 블록 없이 문장 하나만으로도 사용할 수는 있다.   
이 형식은 문장 하나만을 사용하는 점이 장점처럼 보이지만 추후에 작업하는 사람이 쉽게 버그를 만들 수 있으므로 권장하지 않는다.   




### 함수 문장 vs 함수 표현식

- 함수가 선언식으로 (function test(){} ) 선언 될 경우    
함수 문장은 위로 끌어올려지는 대상(호이스팅) 이 되기 때문에   
함수가 위치한 곳과 관계없이 실행될수 있으므로 구조를 엉성하게 만든다.   
함수의 선언을 할 때 표현식 (var test = function(){} ) 를 사용하길 권장한다.   



