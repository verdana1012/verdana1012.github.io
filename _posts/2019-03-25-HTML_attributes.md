---
title: "HTML 전역 속성 사용하기"
categories: posts
tags:
  - html
date: 2019-03-25 00:00:00 -0400
---


전역 속성(Global attributes)은 모든 HTML의 공통 속성이다.

모든 엘리먼트 요소에 사용할 수 있지만 일부 요소에는 효과가 없는 것도 있다.

하나의 엘리먼트의 다중 속성을 선언하는것도 가능하며, 속성을 쓰는 순서도 중요하지 않다.

(자주 사용하거나 익숙한 속성별로 정리하려다가, 그냥 abc 순으로 정리해두었다.)



**[accesskey]**
---

키보드 단축키를 지정하여 해당 엘리먼트를 선택할 수 있게 한다.

accesskey를 설정하는데 필요한 키 조합은 브라우저와 플랫폼마다 차이가 있으며

윈도우에서 대체로 accesskey는 alt키를 함께 누를 때 작동한다.

> ![accesskey image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-25-HTML_attributes_1.png)
> 이미지출처 : https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/accesskey

ex ) 
```
<input type="text" name="name1" accesskey="1">
<input type="text" name="name2" accesskey="2">
```
<input type="text" name="name1" accesskey="1">
<input type="text" name="name2" accesskey="2">

위 인풋태그를 클릭하고 alt + 1  /  alt + 2 를 눌러보면 바로 이해가 될 것이다.

---



**[class]**
---

엘리먼트를 분류할때 쓰인다.

보통 class를 사용하여 CSS로 스타일을 정의하거나

JavaScript에서 class명으로 요소를 선택하거나 접근할 수 있다.

클래스의 이름은 마음대로 지을 수 있지만 의미를 두어 이름을 만드는 것이 좋다.

프로젝트 실무자들과 네이밍을 협의하거나,

CSS 방법론인 SMASS, BEM, OOCSS 등에 맞춰 네이밍을 정하는것을 지향한다.

---



**[contenteditable]**
---

HTML5에서 새롭게 등장한 속성으로 페이지 안에서 사용자들이 컨텐츠를 수정할 수 있게 한다.

속성값을 true로 설정하면 엘리먼트 컨텐츠를 수정할 수 있도록 한다.

ex )
```
<p contenteditable="true">TEST</p>
```

<p contenteditable="true">TEST</p>

위의 **'TEST'** 텍스트는 클릭시 수정이 가능하다.

---



**[contextmenu]**
---

사용자가 엘리먼트의 context menu를 정의할 수 있도록 한다.

사용자가 트리거 했을때 (윈도우의 경우 마우스 우클릭을 했을 경우) 나타난다.

2019년 3월 시점인 지금은 contextmenu 속성을 지원하는 브라우저는 파이어폭스 밖에 없다.


> (브라우저 지원 확인)
> 
> https://www.w3schools.com/tags/att_global_contextmenu.asp


ex )
```
<input type="text" contextmenu="test">
<menu type="context" id="test">
	<menuitem label="테스트111" onclick="alert('111');"></menuitem>
	<menuitem label="테스트222"></menuitem>
</menu>
```

<input type="text" contextmenu="test">

<menu type="context" id="test">
	<menuitem label="테스트111" onclick="alert('111');"></menuitem>
	<menuitem label="테스트222"></menuitem>
</menu>

![contextmenu image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-25-HTML_attributes_2.png)

파이어폭스 브라우저에서 위 인풋을 클릭시 이와같은 사용자 지정 메뉴를 확인할 수 있다.

메뉴에는 onclick과 같은 이벤트를 걸 수 있다.

---



**[data-*]**
---

data- 라고 앞에 붙여 이름을 만듦으로써 사용자 지정 속성을 정의할 수 있다.
사용자 지정 속성은 화면상에 보이지 는 텍스트나 추가정보를 엘리먼트에 담아놓을때 활용할 수 있다.

ex )
```
<input type="text" id="test" data-user="dev" data-number="123">
```

사용자 지정 속성도 HTML 속성이기 때문에 CSS에서 접근할 수 있다. 
CSS의 속성 선택자로 접근하면 쉽다.

```
[data-user='dev']{
  border: 1px solid red;
}
```

javascript 에서 data 속성은 dataset 으로 읽어낼 수 있다.

```
document.querySelector('#test').dataset.user     // "dev"
document.querySelector('#test').dataset.number   // "123"
```

---



**[dir]**
---

엘리먼트 텍스트의 방향을 명시한다.

ltr : 왼쪽에서 오른쪽 방향으로

rtl : 오른쪽에서 왼쪽 방향으로



ex )
```
<p dir="ltr">text</p>
<p dir="rtl">text</p>
```

<p dir="ltr">text</p>
<p dir="rtl">text</p>

---



**[draggable & dropzone]**

HTML5 지원 사항중 하나로, 문서 안의 엘리먼트를 드래그&드랍 할 수 있는지 나타낸다.

(html5 drag & drop 부분은 나중에 더 상세하게 적고, 지금은 간단한 테스트만..)


ex ) HTML
```
<div id="catImg">
  <img draggble="true" id="cat1" src="이미지 url" alt="cat1"/>
  <img draggble="true" id="cat2" src="이미지 url" alt="cat2" />
</div>
<div id="catBox">
    <p>여기로 고양이를 이동</p>
</div>
```


ex ) 스크립트
```
var catImg = document.querySelector('#catImg');
var catBox = document.querySelector('#catBox');
var draggedID;

catBox.ondragenter = handleDrag;
catBox.ondragover = handleDrag;
function handleDrag(e){
    e.preventDefault();
}

//드래그 시작시
catImg.ondragstart = function(e){
    draggedID = e.target.id;
    e.target.classList.add('dragged');
}

//드래그가 끝나는 시점
catImg.ondragend = function(e){
    var elems = document.querySelector('.dragged');
    elems.classList.remove('dragged');
}

//드롭 되면 html을 복사
catBox.ondrop = function(e){
    var newElem = document.getElementById(draggedID).cloneNode(false);
    catBox.innerHTML = "";
    catBox.appendChild(newElem);
    e.preventDefault();
}
```

<p class="codepen" data-height="265" data-theme-id="default" data-default-tab="result" data-user="juein" data-slug-hash="GeepYE" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="drag&amp;amp;drop">
  <span>See the Pen <a href="https://codepen.io/juein/pen/GeepYE">
  drag&amp;drop</a> by juein (<a href="https://codepen.io/juein">@juein</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>





**[hidden]**
---

브라우저에서 엘리먼트를 숨겨준다. 

단순히 뷰만 숨겨지는게 아닌, 브라우저에서 hidden속성의 엘리먼트는 랜더링을 하지 않는다.

---



**[id]**
---

엘리먼트의 유일한 식별자를 부여하기 위해 쓴다.

class처럼 엘리먼트의 스타일을 적용하거나, JavaScript에서 엘리먼트를 선택하기 위해 사용한다.

---



**[lang]**
---

엘리먼트 컨텐츠의 언어를 명시하기 위해 사용한다.

lang 속성을 사용하면 스크린 리더(낭독 프로그램)가 인식하여 텍스트의 적합한 발음을 제공해 주기도 하고

특정 언어에만 스타일을 적용하거나 컨텐츠를 보여주는 활용을 할 수 있다.

ex )
```
<p lang="en">english text</p>
<p lang="ko">한글 텍스트</p>
```

---



**[spellcheck]**
---

브라우저가 엘리먼트 컨텐츠의 철자를 체크해야 할지 명시하기 위해 사용

lang 엘리먼트를 무시하고 철자 체크는 사용자 컴퓨터의 운영체제, 또는 브라우저 설정에서 정의된 언어로 체크한다.

---



**[style]**
---

CSS 스타일을 정의할 때 사용된다.

---



**[tabindex]**
---

HTML 페이지 안에서 'Tab'키로 포커스를 이동할 때의 순서를 정한다.

ex )
```
<input type="text" tabindex="1" placeholder="첫번째">
<input type="text" tabindex="3"  placeholder="세번째">
<input type="text" tabindex="2"  placeholder="두번째">
<input type="text" tabindex="4"  placeholder="네번째">
```

<input type="text" tabindex="1" placeholder="첫번째">
<input type="text" tabindex="3"  placeholder="세번째">
<input type="text" tabindex="2"  placeholder="두번째">
<input type="text" tabindex="4"  placeholder="네번째">

위 인풋에서 **'Tab'** 키를 눌러서 테스트 해보자.

---



**[title]**
---

엘리먼트에 대한 추가적인 정보를 제공하며 보통 브라우저에 tool tip 정보를 표시할때 쓰인다.

ex )
```
<p title="tool tip 텍스트">여기에 마우스를 올려보면 툴팁이 뜬다</p>
```

여기에 마우스를 올려보면 툴팁이 뜬다

---