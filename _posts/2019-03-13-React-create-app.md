---
title: "[React] Windows or CentOS7 / React + create-react-app + yarn + Node js 환경 구축"
categories: posts
tags:
  - React
date: 2019-03-13 00:00:00 -0400
---

React를 사용해보고싶지만 webpack / babel 등을 설정하느라 시간을 투자하기 싫을때  
create-react-app 도구를 사용하면  
React 작업환경을 명령어 하나로 설정 할 수 있다.  

Windows 운영체제와   
CentOS7 (7.4v) 환경에서  
React + create-react-app + yarn + Node js 환경을 구축해보자  



## [Windows에서 환경 구축]

### 1.Node js 설치

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_1.png)

> NodeJs 공식 사이트(https://nodejs.org/ko/download)에서   
> Windows Installer를 내려받아 설치한다.


설치가 끝나면 cmd 창에서 버전확인 및 설치여부 확인이 가능하다.

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_2.png)


### 2. yarn 설치

npm은 의존하는 라이브러리 개수가 많으면 속도가 저하된다.  
yarn은 npm 문제점을 개선한 패키지 매니저로 npm을 대체하여 사용할 수 있다.  

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_3.png)

> 공식사이트(https://yarnpkg.com/en/docs/install#windows-tab) 에서    
> OS와 (Windows 선택) 버전을 선택 후 내려받아 설치한다.

버전은 특별한 이유가 없다면 Stable로 안정된 버전을 받자.   

### 3. create-react-app 설치

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_4.png)


cmd에서 yarn으로 create-react-app을 설치한다.   
나는 설치 시 모든 디렉토리에서 사용하기 위해 global(전역)으로 설치하였다.   

- - - 
#### ※ 리액트 버전 16.8 이후로는 Hooks가 도입되었다. 

> 참고 : https://reactjs.org/docs/hooks-state.html

프로젝트 첫 생성 후 App.js를 확인해보면 차이를 알 수 있는데   


**예전의 코드 (Hooks 미사용)**
```
Class app extends components{
   render (
      return();
   )
}
```

**16.8v 이후의 코드 (Hooks 사용)**
```
function App() {
  return ();
}
```

Hooks를 사용하면 클래스를 사용하지 않아도 되게끔 변경되었다.   
나는 공부하던 책이 class를 사용하는 방식으로 되어있어서 create-react-app 으로 프로젝트 생성 시   
react-scripts 버전을 지정해서 프로젝트를 재생성 하였다.   

```
create-react-app foo --scripts-version react-scripts@^2
```

설치 후 최신 버전으로 업데이트  
```
npm -S react-scripts@^3
```

- - -


### 4. 프로젝트 생성 및 실행

cmd에서 create-react-app 프로젝트명 명령어로 프로젝트를 생성한다.   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_5.png)


생성한 프로젝트 폴더로 디렉토리 이동 후 yarn start를 하면   
NodeJs 기본포트 3000번으로 실행이 된다.   
port 변경은 아래 하단에 [공통](#public)으로 적혀있는걸 참고.   


## [CentOS7 (7.4v) 에서 환경 구축]

### 1. NodeJS 설치

공식사이트를 참고하여 Node js를 설치

> https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora


CentOS7 에서 저장소 할당 후 Node js를 설치하면 된다.   


저장소에 추가   
```
curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
```

Node js 설치   
```
sudo yum install nodejs
```

Node js 설치시 npm은 자동으로 설치된다   


버전 확인   
```
node --version
npm --version
```

### 2. yarn 설치


yarn 설치  
```
sudo npm install yarn -g
```
버전 확인   
```
yarn --version
```


### 3. create-react-app 설치

create-react-app 설치   
```
yarn global add create-react-app
```


### 4. 프로젝트 생성

React 프로젝트 생성 (create-react-app 프로젝트명)   
```
create-react-app test-project
```

### 5. 방화벽 포트 열어주기

CentOS7은 포트를 열어주어야 한다.   
나는 Node js 의 기본 포트인 3000번과 http의 기본포트인 80을 같이 열어놓았다.   

포트허용  
```
firewall-cmd --permanent --zone=public --add-port=3000/tcp
firewall-cmd --permanent --zone=public --add-port=80/tcp
firewall-cmd --reload
```

방화벽 상태도 확인해주자  
```
systemctl status firewalld 
```

public.xml 파일에 직접 입력시 참고  
```
vi /etc/firewalld/zones/public.xml
```

```
<?xml version="1.0" encoding="utf-8"?>
<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="dhcpv6-client"/>
  <service name="ssh"/>
  <port protocol="tcp" port="80"/>
  <port protocol="tcp" port="3000"/>
</zone>
```

방화벽 적용   
```
systemctl reload firewalld
```

방화벽 시작   
```
systemctl start firewalld
```

혹시 ip가 막혀있을수 있다면... 허용 IP 추가   
```
--add-source=<source range>/netmask 옵션을 사용하여 IP 추가
```

ex ) 192.168.1. 대역에서 ssh 접근을 허용시   
```
firewall-cmd --permanent --zone=public --add-source=192.168.1.0/24 --add-port=22/tcp
```

설정 변경후 재시작   
```
firewall-cmd --reload
```

<div id="public">공통</div>
**create-react-app 프로젝트 내에서 포트 변경시**
**생성한 프로젝트 안의 package.json파일 내용 값 중 "start"값 앞에 원하는 포트를 적어주자**

- **Windows**
```
"scripts": { "start": "set PORT=원하는포트 && react-scripts start",
```

- **Linux & Mac**
```
"scripts": { "start": "PORT=원하는포트 react-scripts start",
```


나는 80포트에서 실행하고싶어서 80으로 설정해두었다.   

- Windows 에선  

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_6.png)

- 리눅스에선 요렇게 설정   

![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_7.png)



이제 package.json 파일 위치에서 yarn start로 실행하고  
`http://localhost:설정포트`  
로 접속하면 초기 페이지가 뜬다.  


포트설정을 별도로 하지 않았다면  
`http://localhost:3000`   


나처럼 80포트로 설정해두었다면  
`http://localhost`   
로 접속하면 된다.


![guide image](https://raw.githubusercontent.com/juein/juein.github.io/master/_posts/img/2019-03-13-react_8.png)

정상적으로 뜬다면 셋팅 끝


