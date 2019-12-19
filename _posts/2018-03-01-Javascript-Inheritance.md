---
title: "[JavaScript] 상속"
categories: posts
tags:
  - JavaScript
date: 2018-03-01 00:00:00 -0400
---


## Inheritance (상속)

- 상속의 유용한 점은 코드를 재사용 하는 것이다.    
  새로만든 클래스가 기존 클래스와 매우 유사하다면 상속을 통해 다른 부분만 구현해낼수 있다   
- 자바스크립트는 클래스를 기반으로 하는 상속을 지원하지 않고   
  프로토타입 체인을 이용하여 상속을 구현해낸다. (객체가 다른 객체로 바로 상속 된다)    
  이러한 상속의 구현방식으로 여러가지 패턴이 있다.   


### 의사 클래스 방식(Pseudoclassical)

- 의사 클래스는 클래스처럼 행동하지만 진짜 클래스는 아니다.   
- 클래스가 없는 자바스크립트가 클래스 기반의 상속 방식을 흉내내는 것.    
- 생성자 함수를 통해서 객체를 생성해야 한다.   


<p class="codepen" data-height="693" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="jadjYr" style="height: 693px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="상속 - 의사 클래스">
  <span>See the Pen <a href="https://codepen.io/juein/pen/jadjYr">
  상속 - 의사 클래스</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


- 의사 클래스는 자바스크립트에 익숙하지 않은 프로그래머들에게 편안함을 제공하지만    
자바스크립트의 장점을 가리게 되는 법이다.   
- 위 예제의 문제점으로 모든 객체의 속성이 public 이라는 것과,   
  생성자 함수 new 연산자로 실행하지 않으면 this 바인딩에 의해    
  this는 새로운 객체에 바인딩 되지 않고 전역객체(window)에 연결된다는 문제가 있다.    


### 객체를 기술하는 객체(Object Specifiers)

- 생성자가 매우 많은 매개변수를 갖게되는 경우 생성자가 인수를 받는 대신에    
객체를 기술하는 하나의 객체를 받도록 정의 할 수 있다.   
- 인수는 꼭 순서를 맞출 필요가 없으며, 생성자가 기본값 설정을 잘 하고 있다면 인수를 생략 할 수도 있다.   

```
var test = testFunc( n, c, i, s );
```

위 코드 아래와 같이 작성 할 수 있다.   

```
var test = testFunc({
    name : n,
    color : c,
    idx : i,
    state : s
});
```


### 프로토타입 방식

- 프로토타입에 기반한 패턴에서는 클래스가 필요 없다.   
- 프로토타입에 의한 상속은 클래스에 의한 속성보다 더 간단하다.   


<p class="codepen" data-height="550" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="VrRZZK" style="height: 550px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="상속 - 프로토타입 방식">
  <span>See the Pen <a href="https://codepen.io/juein/pen/VrRZZK">
  상속 - 프로토타입 방식</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>



### 함수를 사용한 방식

- 프로토타입에 의한 상속 패턴의 한가지 단점은 private 속성을 가질수 없다는 것이다.    
(private 변수, private 메소드도 모두 생성할 수 없다.)   
- 함수형 패턴은 유연성이 매우 좋다.  이 패턴은 의사 클래스 패턴보다 작업량이 적고    
캡슐화와 정보은닉에 사용 할 수 있다.   


<p class="codepen" data-height="407" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="RjdPxx" style="height: 407px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="상속 - 함수를 사용">
  <span>See the Pen <a href="https://codepen.io/juein/pen/RjdPxx">
  상속 - 함수를 사용</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>




### 클래스 구성을 위한 부속품

- 제품을 만들 때 부속품을 가져다 조립을 하듯이 객체를 구성할 때도 같은 방법으로 할 수 있다


<p class="codepen" data-height="1259" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="VrRvyV" style="height: 1259px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="클래스 구성을 위한 부속품">
  <span>See the Pen <a href="https://codepen.io/juein/pen/VrRvyV">
  클래스 구성을 위한 부속품</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>