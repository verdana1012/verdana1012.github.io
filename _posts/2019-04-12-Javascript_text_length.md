---
title: "[JavaScript] 글자수 체크, 문자열 길이 구하기(한글 포함)"
categories: posts
tags:
  - JavaScript
date: 2019-04-12 00:00:00 -0400
---


Javascript에서 문자열 길이를 체크할때, 그냥 length를 사용하면  
1Byte인 영문, 숫자 입력시엔 상관없지만  
한글 '가' 입력시에도 length 값은 1로 나온다.  
아래 스크립트는 escape() 함수를 이용해 입력받은 값이 한글인지 판단 후 글자수를 2byte로 계산해준다.  


<p class="codepen" data-height="428" data-theme-id="default" data-default-tab="js,result" data-user="juein" data-slug-hash="GLEMap" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="한글포함 문자열 길이값">
  <span>See the Pen <a href="https://codepen.io/juein/pen/GLEMap">
  한글포함 문자열 길이값</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

