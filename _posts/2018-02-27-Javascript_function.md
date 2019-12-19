---
title: "[JavaScript] 함수"
categories: posts
tags:
  - JavaScript
date: 2018-02-27 00:00:00 -0400
---

## Function (함수)


- 함수는 실행 문장들의 집합을 감싸고 있다.   
- 함수는 코드의 재사용이나 정보의 구성 및 은닉화 등에 사용할 수 있고 객체의 행위를 지정하는데도 사용한다.   


### 함수 객체

- 자바스트립트에서 함수는 객체이기 때문에 다른 값들처럼 사용 할 수 있다.   
변수, 객체, 배열 등에 저장될 수 있고, 다른 함수에 전달하는 인수로도, 반환값으로도 사용 할 수 있다.    
- 함수를 다른 객체와 구분 짓는 특징은 '호출' 할 수 있다는 점이다.   
- 객체는 Object.prototype 에 연결되지만 함수는 Function.prototype 에 연결된다.   
 함수객체의 prototype 속성에 함수 자체를 값으로 갖는 생성자(constructor) 속성이 있다.   
(생성자는 객체 생성시에 호출되며 메모리 생성과 객체 데이터의 초기화를 한다. 생성자에 대한 자세한건 나중에...)   


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_1.png)



### 함수 리터럴

- 함수 리터럴은 표현식이 나올 수 있는 곳이면 어디든지 위치할 수 있다.   
- 함수는 다른 함수 내에서도 정의할 수 있다.   
- 함수 리터럴로 생성한 함수 객체는 외부 문맥으로의 연결이 있는데 이를 클로저(closure) 라고 한다.   

```
//선언문 방식(반드시 함수명이 정의되어야 함)
function test1( a, b ){

  var r = a + b;
  console.log(r);

}

// 기명함수 호출
test1( 1, 2 );
//표현식 함수선언
var test2 = function( a, b ){

  var r = a + b;
  console.log(r);

}

// 함수 호출
test2( 1, 2 );
```


- 위의 선언식, 표현식 외에 자바스크립트 함수도 Function() 기본내장 생성자 함수로부터 생성된    
'객체' 이기 때문에Function() 생성자 함수로 함수를 생성하는 법이 있다.   

```
//생성자 함수로 함수를 생성
var test3 = new Function ( 'a', 'b', 'return a+b' );

//함수호출
console.log(test3(1,2));
- 함수를 정의함과 동시에 바로 실행하는 즉시 실행 함수도 있다.

//즉시 실행 함수
(function (test){
  console.log(test);
})('test_text');
```


### 호출

- 함수 호출에는 네가지 패턴이 있다. (메소드 호출, 함수 호출, 생성자 호출, apply 호출)   
- 메소드 호출 패턴 (함수를 객체의 속성에 저장하는 경우, 그 함수는 '메소드' 라 부른다.)   

```
var say = function(something){
    console.log(something);
}

say('hello');
```

- 생성자, apply 호출 패턴   
call과 apply 함수는 자바스크립트만의 독특한 내장 함수로,    
Function 객체에 기본적으로 들어있는 함수이다. (정확히 말하자면 Function.prototype에 들어있는 함수)   
apply 호출은 생성자 호출과 비슷하지만 인수들을 배열로 넘겨주는데에 차이가 있다.   

```
var say = function(something){
    console.log(something);
}

say.call(undefined, 'call hello'); // 생성자 호출
say.apply(undefined, ['apply hello']); // apply 호출
```


- 모든 함수에는 this와 argument라는 추가적인 매개변수 두 개를 받게되는데,    
자바스크립트 에서 this라는 매개변수의 값이 호출하는 패턴에 따라 바뀐다.   
위의 네가지 패턴에 따라 this라는 매개변수의 값이 다르게 초기화 된다.   
this 바인딩에 대한 이해는 확실하게 공부 후 적겠음 ㅠㅠ   



### 인수 배열(arguments)


- 함수를 호출할 때 this와 같이 추가적으로 매개변수로 arguments 배열을 사용하게 된다.   
타 언어와 달리, 자바스크립트에서는 함수를 호출할 때   
함수 형식에 맞춰 인자를 넘기지 않더라도 에러가 발생하지 않는데,    
이러한 이유는 암묵적으로 argument 객체가 함수 내부로 전달되기 때문이다.   

```
var test_func = function( num1, num2 ){
    console.log(num1, num2);
};

test_func();        // undefined undefined 출력
test_func(1);       // 1 undefined 출력
test_func(1,2);     // 1 2 출력
test_func(1,2,3);   // 1 2 출력
```


위 함수를 `console.dir(argument)` 로 실행해서 보면   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_2.png)


함수 호출 시 넘겨진 인자가 배열 형태로 저장되어 있다.   
추가적으로 arguments는 length 속성이 있지만 실제 배열이 아닌 객체다.    
(length를 제외한 배열이 가지는 메소드들이 없다.)   


### 반환
- 함수는 몸체를 닫는 } 를 만나면 함수가 끝나면서 함수를 호출한 부분으로 값이 반환된다.   
- 함수의 뭄체 안에서 return 문을 사용하면 } 에 도달하기 전에 값을 반환 할 수 있다.   
- 반환값을 저장하지 않은 경우에는 undefined가 반환된다.   

```
var test_func = function(){
    return console.log('return text');

    console.log('default text');
}

test_func();   // return text 출력
```


### 예외

- 자바스크립트는 예외를 다룰 수 있는 메커니즘을 제공한다.  
  예외란 정상적인 프로그램의 흐름을 방해하는 비정상적인 사고를 말한다.(오류발생)  
- try~ catch 문은 try 블록 내에서 예외가 발생하면, catch 블록이 실행된다.  

<p class="codepen" data-height="490" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="XzZrOM" style="height: 490px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="try_catch">
  <span>See the Pen <a href="https://codepen.io/juein/pen/XzZrOM">
  try_catch</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>



### 기본 타입에 기능 추가

- 모든 객체가 연결되어있는 prototype 에 기능(메소드)을 추가하는것이 가능하다.   

```
var person = function( name, age ){

}

console.dir(person);
```

`console.dir(person)` 출력시 콘솔창의 모습

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_3.jpg)


위 함수에 prototype 추가   

```
person.prototype.eyes = 2;
person.prototype.mouth = 1;
```

`console.dir(person)` 출력시 콘솔창의 모습   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_4.jpg)


이러한 방법으로 기본적인 타입에 기능을 추가 할 수 있다.   

- 프로토타입에 메소드를 추가하면 메소드가 추가되기 전에 생성되었던 값들에게도 바로 적용된다.   
- 기본타입의 프로토타입은 public 구조이므로   

```
if( !person.prototype.eyes ){

person.prototype.eyes = 2;
    
}
```


위와 같이 추가하려는 값이 존재하지 않을 때에 메소드를 추가하는 방식으로 하면 좋다.   


### 재귀적 호출

- 함수 안에서 자기 자신을 호출하는것을 재귀적 함수 호출(Recursive Function Call), 간단하게 재귀(Recursion) 라고 한다.    
- 재귀함수의 쉬운 예로, 수열 앞에 나오는 두 개의 숫자를 더해가는 피보나치 수열을 예제로 든다.   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_5.png)


```
var fibonacci = function( n ){

 if( n === 0 || n === 1 ){
    return 1;
  }else {
    return fibonacci(n-1) + fibonacci(n-2);
  }
}

for (var i = 0; i < 10; i++){
  console.log( fibonacci(i) );  // 1, 1, 2, 3, 5, 8, 13, 21, 34, 55 출력
}
```


위 예제에서 눈여겨 볼 부분은 함수 안에서 자기 자신을 호출하는것이 가능하다는 점이다.   



### 유효범위(Scope)

- 유효범위는 이름들이 충돌하는 문제를 덜어주고 자동으로 메모리를 관리하기 때문에 중요하다.   
- C언어 유형의 구문을 가진 언어들은 블록 `{}` 유효범위가 있어서 `{}` 내에서 정의된 모든 변수는 `{}` 바깥쪽에서 접근할 수 없는 구조로 되어있지만 자바스크립트 에서는 `{}`은 유효범위를 지원하지 않는다.   
- `{}` 유효범위는 없지만 함수 유효범위는 존재한다.    
함수 내부에서 선언한 변수와, 함수의 매개변수는 함수 외부에서 유효하지 않는다.    


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_6.png)


```
var test = function(){
  var b_text = "bbbbb"; //지역변수, var 선언 안하면 전역변수가 된다.
  document.write("함수 내에서 출력 : " + a_text );
}

test();
document.write("함수 밖에서 출력 : " + a_text );

```



### 클로저 (closure)

- 내부함수에서 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있는것을 클로저 라고 한다.   
  다른 의미로 이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 함수 자체가 클로저다.   

```
var out_func = function(){

  var a = 10;    // <-- 자유변수

  return function(){    // <-- 클로저

    //a 를 활용한 로직(클로저)
    console.log( a + ' add text' );

  };

};
```


위 예제에서 out_func에 선언된 변수 a 를 참조하는 함수가 클로저가 된다.   
그리고 클로저로 참조되는 외부변수, 즉 out_func의 a와 같은 변수를 '자유변수' 라고 한다.   

클로저에 대한 예를 하나 더 보자면   

```
//클로저를 사용하지 않은 코드
var count = 0; //전역변수

window.onload = function(){

  var button = document.getElementById('btn');
  button.onclick = btn_click;

}
```

```
var btn_click = function(){

  count ++;
  console.log( count +'번 클릭 (클로저 사용 안함)');

}

//클로저를 사용
window.onload = function(){

  var count = 0; // <-- 자유변수
  var button = document.getElementById('btn');

  button.onclick = function(){  // <-- 클로저

    count ++;

    //button.onclick 속성에 할당된 함수에 대한 클로저를 생성
    console.log( count +'번 클릭 (클로저를 사용)');

  };

}
```


위 예제의 클로저 사용 부분을 보면   
버튼을 클릭하는 onclick 속성에 클로저가 할당 된다.   
외부 함수에 있는 button 변수는 window.onload 함수가 종료될때 사라졌지만   
button 객체는 onclick 속성에 저장된 클로저를 갖고 있다.   



