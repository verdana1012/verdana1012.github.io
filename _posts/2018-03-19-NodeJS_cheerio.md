---
title: "[Nodejs] request와 cheerio를 이용한 웹페이지 크롤링"
categories: posts
tags:
  - NodeJS
date: 2018-03-19 00:00:00 -0400
---



## request와 cheerio를 이용한 웹페이지 크롤링


### request 모듈 : 웹 페이지를 받아오는 모듈

### cheerio 모듈 : HTML 문자열을 jQuery 객체로 만들어주는 모듈


HTML 데이터를 request로 가져오고, 크롤링 한 HTML 데이터를 파싱하기 위해 cheerio를 사용한다.   



#### request 와 cheerio 모듈 설치

```
npm install request && install cheerio
```


긁어올 html파일 구조   

```
<div>
    <li class="web_page_list">
        <p class="number">0000</p>
        <p class="name">test</p>
    </li>
</div>
```


js파일   

```
//모듈 추출
var request = require('request');
var cheerio = require('cheerio');

//request 모듈 사용
var url = '웹페이지주소';
request(url, function(err, response, body){
    //변수 선언
    var $ = jQuery = cheerio.load(body);

    //데이터 추출
    $('.web_page_list').each(function(item){

        var number = $(this).find('.number').text().trim();
        var name = $(this).find('.name').text().trim();
        console.log(number);
        console.log(name);
        
    })
});
```

