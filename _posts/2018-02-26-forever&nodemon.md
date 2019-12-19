---
title: "forever & nodemon & supervisor"
categories: posts
tags:
  - NodeJS
date: 2018-02-26 00:00:00 -0400
---


**forever, nodemon, supervisor 이런 모듈은 전역 모듈이므로 -g 옵션을 사용하여 한번만 설치하면 된다.**


### [forever]

Node.js 는 단일 스레드 기반이여서 예외가 하나라도 생긴다면 웹 서비스 전체가, 서버가 죽어버린다.   
이러한 예외 상황을 대비하고자 만들어진 모듈이 forever 모듈이다.  
예외가 발생하여 웹 서버가 죽어도 다시 지속적으로 실행하게 해주는 관리 모듈이다.  


설치
```
npm install -g forever
```


기본 명령어 확인
```
forever
```

실행
```
forever start app.js
```


재실행
```
forever restart app.js
```


실행중지
```
forever stop app.js
```

실행중인 모든 데몬 정지
```
forever stopall
```

실행 프로세스 리스트 보기
```
forever list
```

npm start 경로 및 실행
```
forever start -c "npm start" ./bin/www
```


### [nodemon]

nodemon이 시작된 디렉토리의 파일이 변경되면(수정되면) 자동으로 restart 해준다.   


설치
```
npm install nodemon -g
```


기본 명령어 확인
```
nodemon --help
```


app.js 자동 재실행
```
nodemon app.js  
```

forever와 같이 사용할경우
forever start -c nodemon ./bin/www

 

### [supervisor]

nodemon과 비슷한 모듈로, 파일의 변경사항을 자동으로 인식하여 재시작 해준다.    
nodemon, supervisor 둘 중 하나만 설치하여 사용해도 무방함.  


설치
```
npm install supervisor -g
```

기본 명령어 확인
```
supervisor
```


app.js 자동 재실행
```
supervisor app.js
```

