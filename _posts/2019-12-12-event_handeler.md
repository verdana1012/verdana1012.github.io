---
title: "[JavaScript] 이벤트 핸들러 1번만 적용하고 제거하기"
categories: posts
tags:
  - JavaScript
date: 2019-12-12 00:00:00 -0400
---



### 기본적인 이벤트 핸들러의 선언 및 제거방법

```
//실행 될 이벤트
function test(){}

이벤트 핸들러 선언
element.addEventListener("click", test);

이벤트 핸들러 제거
element.removeEventListener("click", test);

익명함수를 콜백으로 쓰게 될 경우엔
element.addEventListener("click", function(){
 test();
 
 // 선언한 클릭이벤트가 전부 제거 되어버림	
 this.removeEventListener("click");  
 
 // arguments.callee 를 사용하면 원하는 이벤트만 제거
 this.removeEventListener("click",arguments.callee);  

});
```


removeEventListener 활용 예)    
비디오 재생 여부를 timeupdate 이벤트로 판별할 때   
이벤트 핸들러를 제거하지 않으면 해당 이벤트가 계속 실행되니   
removeEventListener 를 잘 활용해주자   


<p class="codepen" data-height="483" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="QWwEyYX" style="height: 483px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="video play image">
  <span>See the Pen <a href="https://codepen.io/juein/pen/QWwEyYX">
  video play image</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>