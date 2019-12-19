---
title: "[JavaScript] 콜백, 모듈, 커링, 메모이제이션"
categories: posts
tags:
  - JavaScript
date: 2018-02-28 00:00:00 -0400
---


## 콜백, 모듈, 커링, 메모이제이션


### 콜백

- 이름이 없어 호출하지 못하는 익명함수의 대표적인 용도가 콜백 함수다.   
- 콜백함수는 코드를 통해 명시적으로 호출하는 함수가 아니라   
어떠한 이벤트가 발생했을때, 특정 시점에 도달했을때 시스템에서 호출되는 함수다.   
대체로 이벤트 핸들러가 콜백 함수로 등록되는 경우가 많다. (이벤트 핸들러는 'on + 이벤트명' 으로 지어져있다.)   

```
//페이지 로드시 호출퇼 콜백함수
window.onload = function(){
  document.write('browser load~');
}

//버튼 클릭시 호출될 콜백함수
document.getElementById("test").onclick = function() {
  document.write('button click~');
};
```


이벤트 핸들러가 아닌 콜백 함수의 예로는


<p class="codepen" data-height="480" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="qVoLbQ" style="height: 480px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="콜백">
  <span>See the Pen <a href="https://codepen.io/juein/pen/qVoLbQ">
  콜백</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>




### 모듈

- 타 언어에서는 접근 제한자(public, private 등..) 이 있지만 자바스크립트에는 존재하지 않아   
클로저와 스코프 개념을 통해서 접근제한자의 특징을 흉내낼 수 있다.   
기본적인 모듈 패턴의 예로   

<p class="codepen" data-height="957" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="ooMmbm" style="height: 957px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="모듈 패턴">
  <span>See the Pen <a href="https://codepen.io/juein/pen/ooMmbm">
  모듈 패턴</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

inCounter() 가 동일한 메서드 이름을 사용하지만 전혀 다른 스코프상에 존재하는 다른 값이다.  
- testModule_1 , testModule_2 의 내부 리소스는   
해당 모듈 이름 testModule_1 , testModule_1를 통해서만 접근이 가능하다.  
- 모듈에서 return 되지 않은 대상은 접근이 불가능하다.  




### 연속 호출(Cascade)

- 자바스크립트 에서 메소드의 반환값이 this 라면 연속 호출이 가능하다.   

<p class="codepen" data-height="642" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="MOBRQj" style="height: 642px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="연속호출">
  <span>See the Pen <a href="https://codepen.io/juein/pen/MOBRQj">
  연속호출</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


연속호출은 한번에 많은 작업을 할 수 있는 이너페이스를 만드는데 도움이 된다.   



### 커링(Curry)

- 커링이란 특정 함수에서 정의된 인자의 일부를 넣어 고정시키고, 나머지를 인자로 받는 새로운 함수를 만드는 것을 말한다.   

<p class="codepen" data-height="475" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="zPLQrj" style="height: 475px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="커링">
  <span>See the Pen <a href="https://codepen.io/juein/pen/zPLQrj">
  커링</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


위 예제로 만들어진 `curry()` 함수의 역할은   
`curry()` 함수로 넘어온 인자를 args에 담아놓고, 새로운 함수 호출로 넘어온 인자와 합쳐서 함수를 적용한다.   




### 메모이제이션(Memoization)

- 메모이제이션은 계산 결과를 함수의 프로퍼티 값으로 담아놓고 나중에 사용할 수 있다.   
- 함수의 연산된 값을 저장해두므로 중복 연산을 피할 수 있어 불필요한 작업을 줄일 수 있다.   

재귀함수때 잠깐 봤던 피보나치 수열로 다시 예를 들자면


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2018-02-26-Javascript_5.png)


<p class="codepen" data-height="1124" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="rYZqpd" style="height: 1124px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="메모이제이션">
  <span>See the Pen <a href="https://codepen.io/juein/pen/rYZqpd">
  메모이제이션</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>

위 코드는 문제가 없으나, 수열의 10번째 칸 까지의 계산을 할때 fibonacci_1() 함수가 276번이나 호출된다.

이 코드에 메모이제이션 패턴을 사용해서 보면

수열의 10번째 칸 까지의 계산을 할 때   
fibonacci_1() 함수는 276번이나 호출되지만    
메모이제이션 패턴을 적용한 fibonacci_2() 함수는 26번만 호출된다.   
fibonacci_2() 함수는 호출되면 제일 먼저 결과가 저장되어 있는지를 확인 한 후   
저장된 값이 있으면 연산을 수행하지 않고 바로 결과를 반환한다.



