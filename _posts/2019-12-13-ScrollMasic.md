---
title: "[JS - Plugin] Scroll Masic"
categories: posts
tags:
  - Plugin
date: 2019-12-13 00:00:00 -0400
---

### Scroll Masic Plugin   

> 라이센스 : [MIT] License
> 공식문서 : http://scrollmagic.io/docs



### 한눈에 보는 Cheat Sheet   

![Cheat Sheet](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-12-13-img_1.png)



스크롤매직을 제대로 활용하려면 doc문서를 참고하는게 좋다.   
밑에는 자주 쓰는 기능만 간단하게 설명   

 
```
//컨트롤러 선언
var ctrl = new ScrollMagic.Controller();

new ScrollMagic.Scene({
	reverse: true, //false : 한번만 적용, 기본값 : true
	triggerElement: this, // 컨텐츠 영역. '#project01 img', 등 원하는 요소로 바꿀 수 있다.
	//reverse : true 설정시 스크롤 상/하 움직임이 반전된다.
	duration: '100%',
	//duration: '100%', // duration:$("#intro").height() 등 동작하는 구간을 설정하여 end 생성,
	// 숫자로 줄때는 따옴표 없이, %로 줄때는 따옴표 넣고  %를 주면 뷰포트의 %값으로 동작
	// ex ) ex. duration: 300 / duration: '100%'
	triggerHook: 0.25 //0은 뷰포트의 최상단, 1은 뷰포츠의 최하단으로 trigger 팁이 이동
	// 0.9 설정시 뷰포트에서 보여질 때 fade in, 뷰포트에서 벗어날 즈음 fade out되는 효과를 가진다.
}).setTween(testTween) //tween 실행
.setClassToggle('box', 'test') // 원하는곳에 클래스 추가 (box 클래스에 test 클래스추가)
.addIndicators({
		name: 'test scene', //팁 이름, 기본값 넘버링
		colorTrigger: "white", //트리거 팁 색상
		colorStart: "white", //스타트 팁 색상
		colorEnd: "white", //종료 팁 색상
		indent: 40 //우측 스크롤바부터 얼마나 떨어뜨릴지
})
.on("start end", function (e) { // 스크롤 이벤트 발생지점에서 콜백 함수를 던져준다. (type, state 등..)
    console.log(e);
});
.addTo(ctrl);
```
 

### 기본 사용 예제  

#### 1) 지정한 위치에 스크롤(triggerHook 지정위치) 에 도달하면 Tween 실행  


<p class="codepen" data-height="400" data-theme-id="default" data-default-tab="result" data-user="juein" data-slug-hash="rNaLLav" style="height: 400px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="ScrollMasic guide (1)">
  <span>See the Pen <a href="https://codepen.io/juein/pen/rNaLLav">
  ScrollMasic guide (1)</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


#### 2) 위 예제의 반복효과를 원할 경우엔 이런 식으로 사용 할 수도 있다.   

<p class="codepen" data-height="400" data-theme-id="default" data-default-tab="result" data-user="juein" data-slug-hash="BayzzRp" style="height: 400px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="ScrollMasic guide (2)">
  <span>See the Pen <a href="https://codepen.io/juein/pen/BayzzRp">
  ScrollMasic guide (2)</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
<br>


#### 3) pin을 활용하면 시각적으로 가로스크롤이 되는 것 처럼 활용도 가능   


<p class="codepen" data-height="400" data-theme-id="default" data-default-tab="result" data-user="juein" data-slug-hash="BayzzOZ" style="height: 400px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="ScrollMasic guide (3)">
  <span>See the Pen <a href="https://codepen.io/juein/pen/BayzzOZ">
  ScrollMasic guide (3)</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>