---
title: "[JavaScript] 객체"
categories: posts
tags:
  - JavaScript
date: 2018-02-26 00:00:00 -0400
---

## Object (객체)

- 객체는 변형 가능한 속성들의 집합. 객체는 그저 속성을 모아놓은 것이다.   
(숫자, 문자, 불리언, null, undefined 를 제외한 값들은 모두 객체다, 배열, 함수, 정규표현식 등은 모두 객체!)   
- 객체의 속성명은 문자열이면 모두 가능하다. 빈 문자열도 가능.   
- 속성값은 undefined를 제외한 모든 값이 사용가능   
- 자바스크립트 객체는 클래스가 없지만, 다른 객체에 상속하게 해주는 프로토타입(prototype) 이 있다.   
이 특성을 잘 활용하면, 객체를 초기화하는 시간과 메모리 사용을 줄일 수 있다.   

<p class="codepen" data-height="265" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="ooLzQw" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="object ">
  <span>See the Pen <a href="https://codepen.io/juein/pen/ooLzQw">
  object </a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

   
### 객체 리터럴   
- 중괄호 `{}` 로 둘러싸고 이름/값 쌍으로 표현하고, 속성:값 의 쌍들을 구분하는데에 `,` 를 사용   
```
var car = {
  'color' : 'black',
  'model' : 'avante',
  'year' : '2010',
  'wheel' : 4
};
```

### 속성값 읽기
- 대괄호 `[]` 로 둘러싸거나, 마침표 `.` 표기법으로 읽기 가능   
```
document.write( car['name'] );
document.write( car.name );
```

- (존재하지 않는 값을 읽으려고 하면 undefined 를 반환하는데,    
`||` 연산자를 사용하여 undefined 외에 출력되는 기본값을 지정해 줄 수 있다   
```
document.write( car.window || "no window" );
```

### 속성값의 갱신

- 객체의 값은 할당에 의해 갱신된다. 이미 객체안에 존재하면 해당 속성의 값이 변경된다.    

```
// 이미 존재하는 값에 값을 할당 : 속성 값 갱신
car['color'] = 'white';

// 새로운 속성 값 할당 : 객체의 속성 값 추가
car['make'] = 'hyndai';
```


### 참조

- 객체는 참조 방식으로 전달된다. 복사되는게 아니다.

```
var a = { number : 10 };
var b = a;

document.write(a.number); // 10 출력
document.write(b.number); // 10 출력

b.number = 20;

document.write(a.number); // 20 출력
document.write(b.number); // 20 출력
```

위 예제에서 변수 a는 객체 자체를 저장하고 있는 것이 아니라    
생성된 객체를 가리키는 참조값으로 저장되어있으므로   
같은값을 참조하는 b의 변수가 변경되면   
a의 값도 같이 바뀐다.   



### 프로토타입(Prototype)

- 자바스크립트의 모든 객체는 자신의 부모 역할을 하는 객체(Object)와 연결 되어있다.   
- Object.prototype 에는 toString(), valueOf() 등과 같은 모든 객체에서 호출 가능한 기본 내장 메서드가 포함 되어있다.   
이를 상속받은 객체에서 Object.prototype 에 있는 다양한 메서드를 마치 자신의 속성인것 처럼 사용 할 수 있다.   
- console.dir() 로 지정된 객체의 프로토타입을 쉽게 확인 가능   





### 리플렉션

- 변수의 타입을 체크하고 객체의 구조를 탐색하는 과정을 리플렉션 이라 한다.   
- 쉬운 방법으로 typeof 연산자를 사용하여 객체에 어떤 속성들이 있는지 확인 할 수 있다   

```
document.write(typeof car.color);  // string 출력
document.write(typeof car.wheel);  // number 출력
```

- 원하지 않는 속성을 배제하기 위해 hasOwnProperty 메소드를 사용하는 방법이 있다.   
(hasOwnProperty 메소드는 객체에 특정 속성이 있는지 확인해서 true/false 값을 반환해주는 메소드로,    
이 메소드를 사용하면 프로토타입 체인을 바라보지 않는다.)   

```
document.write(car.hasOwnProperty('color'));   // true 출력
```

### 열거(Enumeration)

- for in 구문을 사용하여 객체에 있는 모든 값의 속성 이름을 늘어놓을 수 있다.    

<p class="codepen" data-height="354" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="rYLmEp" style="height: 354px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="car object">
  <span>See the Pen <a href="https://codepen.io/juein/pen/rYLmEp">
  car object</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


### 삭제

- delete 를 사용하여 객체의 속성을 삭제 가능하다.   
(delete는 프로토타입 연결상에 있는 객체들은 접근하지 않는다.)   

```
delete car.wheel;
```


### 최소한의 전역변수 사용

- 전역변수의 잦은사용은 프로그램의 유연성을 약화하기 때문에 가능하면 피하는것이 좋다.    
전역변수 사용을 최소화 하는 방법중 하나로, 먼저 전역변수 하나를 생성 한 후    
선언한 변수를 다른 전역변수를 위한 컨테이너로 사용하는 방법이 있다.   

```
var car = {};

car.avante = {
    'color' : 'black',
    'make' : 'hyndai'
};

car.sorento = {
    'color' : 'white',
    'make' : 'kia'
};
```

- 이러한 방법으로 전역변수를 이름 하나로 관리하면    
다른 라이브러리들과 연동할 때 발생하는 문제점을 최소화 할 수 있다.   
- 전역변수 사용을 줄이는데 효과적인 방법으로 클로저 사용이 있는데 그건 나중에..   




