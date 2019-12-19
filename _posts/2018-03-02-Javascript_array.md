---
title: "[JavaScript] 배열"
categories: posts
tags:
  - JavaScript
date: 2018-03-02 00:00:00 -0400
---


## Array (배열)

- 자바스크립트에서 배열은 연속적인 메모리 할당이되는 진짜 배열이 아니고  배열같은 특성을 지닌 객체를 제공해 주는 것이다.   
- 실제 배열보다 속도는 느리지만 사용하기 편리함에는 변함이 없다.   
- 배열 전용 유용한 메소드들이 있다. (sort, 값 추가제거, 인덱스 찾기 등..)   


### 배열 리터럴

- 배열 리터럴은 타 언어 배열 선언과 마찬가지로 [] 를 사용하여 선언한다. ( var arr = []; )   
- 타 언어에서의 배열은 한 배열의 구성요소가 같은 데이터타입 이여야 하지만   
  자바스크립트 에서는 어떠한 데이터 타입의 조합도 가능하다.    
  [1, 'string', NaN, undefined, true, false, 10.1]...   
- 객체와 배열은 유사해 보이지만, 생성시 상속받는 prototype이 다르다.   

```
//객체
var test = {
  'test_1' : '111',
  'test_2' : '222',
  'test_3' : 333,
  'test_4' : 444
};

//배열
var arr = [
  'test_5', 'test_6', 777, 888
];
```


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-03-02-Javascript_1.png)


### length 속성

- 모든 배열은 length 속성이 있다.   
- length속성은 사실 실제 배열의 개수를 새는것이 아니라 배열의 가장 큰 속성값보다 하나 더 큰 값으로 되어있기 때문에   
  length의 값이 배열에 있는 속성의 수와 반드시 일치하는 것은 아니다.   

```
//length의 값은 실제 속성의 수와 일치하지 않는다.
var test_arr = [];
console.log(test_arr.length);  // <-- length: 0 출력

test_arr[1000] = true;
console.log(test_arr.length);  // <-- length: 1001 출력
```


### 삭제

- 자바스크립트의 배열은 실제론 객체이기 때문에 delete 연산자로 배열의 요소를 삭제할 수 있다.   

```
var arr = [
  'string_1', 'string_2', 333, 444
];

//배열의 요소를 delete로 삭제
delete arr[0];
console.log(arr); // <-- [undefined, "string_2", 333, 444] 로 출력된다.
```

- 하지만 배열을 delete 연산자로 삭제를 하게 되는 경우 값이 undefined로 될 뿐 값이 완전히 사라지지 않는다. (length 속성의 변화가 없다)   
- 완전한 배열 요소 삭제를 위해선 splice() 메소드로 배열을 변경할수 있다.   

```
var arr = [
  'string_1', 'string_2', 333, 444
];

//배열의 요소를 splice를 사용하여 배열 일부를 삭제
arr.splice( 0 , 1 );
console.log(arr); // <-- ["string_2", 333, 444] 출력
```


### 열거

- 일반 객체를 열거할때 for in 문으로 열거를 하였지만 배열을 for in 문으로 열거하게 되면 프로토타입 체인에 있는 
예상치 못한 속성을 열거 할 수도 있어서 배열은 일반 for문으로 열거한다. (배열의 length 속성으로 반복 횟수의 조건을 준다)

<p class="codepen" data-height="558" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="jYNWoP" style="height: 558px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="배열 열거">
  <span>See the Pen <a href="https://codepen.io/juein/pen/jYNWoP">
  배열 열거</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


### 객체와 배열의 혼동

- 객체는 {} 로 감싸여있고 키(Key)와 값(Value)로 이루어진 속성들로 구성되어있고    
배열은 [] 로 감싸여있으며 배열 안에 들어간 것들은 요소(item) 이라고 한다.   
- 배열이 객체와의 차이점은 키(Key)가 없다는 점이다.    
- 일반적으로 코드를 작성할때 속성 이름이 작은 크기의 연속된 정수이면 배열을 사용하고 그렇지 않은 경우에 객체를 사용하는 규칙을 이용한다.   



### 배열의 메소드

- 배열에 동작하는 메소드들중 자주쓰는 몇가지를 알아보자.     

<p class="codepen" data-height="485" data-theme-id="default" data-default-tab="js" data-user="juein" data-slug-hash="wpwGJa" style="height: 485px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="배열 메소드">
  <span>See the Pen <a href="https://codepen.io/juein/pen/wpwGJa">
  배열 메소드</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


### 배열의 크기와 차원

- 타 언어에서는 1차원배열, 2차배열, 3차배열...다차원 배열을 사용 할 수 있지만
  자바스크립트에서는 배열이 객체이기 때문에 다차원 배열을 지원해주진 않는다.
  떄문에 요소 안에서 다시 배열을 선언해 주는 방법으로 다차원 배열을 구현한다. (배열안의 배열 형태)

```
var arr = new Array();

arr[0] = new Array();    // <-- 배열 안에서 2차배열 선언
arr[1] = new Array(); 

arr[0][0] = " string 111";
arr[0][1] = 111;

arr[1][0] = "string 222";
arr[1][1] = 222;

console.log(arr);
```

console.log(arr); 의 출력결과   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-03-02-Javascript_1.png)


- 위 방법 또는 배열 리터럴로 2차배열을 쉽게 생성할 수 있다.   

```
var arr = [
  [ 0, 1, 2 ],
  [ 3, 4, 5 ],
  [ 6, 7, 8 ]
];

console.log( arr[2][0] ); // <-- 2차원 배열의 요소 읽기, 6 출력
```


- 2차원 배열을 이해하기 쉬운방법중 하나로 구구단을 출력해 볼 수 있다.    


<p class="codepen" data-height="449" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="QaLNZp" style="height: 449px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="다차원 배열">
  <span>See the Pen <a href="https://codepen.io/juein/pen/QaLNZp">
  다차원 배열</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>