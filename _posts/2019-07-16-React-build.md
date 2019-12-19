---
title: "[React] create-react-app 작업 내용을 build 하기"
categories: posts
tags:
  - React
date: 2019-07-16 00:00:00 -0400
---

빌드를 하면 react 소스를 js 소스로 변환할 수 있다.  
즉 NodeJs / React가 구축되어있지 않은 환경에서 동작도 되고, 소스 압축도 해준다.  
빌드 하는 방법은 매우 간단하다.  

먼저 package.json 파일 하단에 "homepage" : "원하는 경로" 를 적어준다.  
homepage 에 대한 안내 설명은 하단 링크를 참고한다.   

> https://github.com/facebook/create-react-app/blob/master/docusaurus/docs/deployment.md#building-for-relative-paths


나는 상대경로를 사용하기 위해 "homepage": "./", 로 설정하였다.   


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-07-16-react_1.png)


경로 설정 후 yarn build 명령어를 입력하면 끝이다.   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-07-16-react_2.png)

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-07-16-react_3.png)

빌드가 끝나면 프로젝트 내에 build 폴더가 새로 생성된 것을 확인 할 수 있다.   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-07-16-react_4.png)

빌드 된 index.html을 실행해보면 결과물을 확인 할 수 있다.   


