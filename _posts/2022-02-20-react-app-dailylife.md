---
title: React 웹앱 구현하기 with 생활코딩
date: 2022-02-20 18:00:00 +/-TTTT
categories: [Web, React]
tags: [html, css, javascript, reactjs, frontend, 생활코딩]
---
## <span style="color:#3498db">**npm**</span> 그리고  <span style="color:#3498db">**npx**</span>
npx 명령어를 사용해서 패키지를 설치할 때도 있고, npm 명령어를 사용해서 할 때도 있다. 
둘 사이의 차이점이 모호할 때가 종종 있는데 무슨 차이가 있는지 알아볼 필요가 있다.

깊게 들어가보면 많은 차이가 있겠지만, 중점적으로 알면 좋을 것들만 알아보자.

npx는 새로운 패키지 관리 모듈은 아니다. 기존 자바스크립트 패키지 관리 모듈인 npm(Node Package Module)의 5.2.0 버전부터 npm에 추가가 되었는데, 이는 npm의 단점을 보완해 npm을 더 편히 사용하게 해주는 도구임을 의미한다.

### npx란
npx는 npm에 올라가있는 패키지를 쉽게 설치하고 관리할 수 있게 도와주는 CLI 도구이다. npm을 통해 설치할 수 있는 모든 종류의 node.js기반 파일들을 간단하게 설치 및 실행할 수 있게 도와준다.

기존 npm의 단점으로는 굉장히 변화가 심한 자바스크립트 생태계에서 전역이나 로컬에서 설치해 관리하게 되면 관리가 되게 쉽지 않다는 점이 있었다.

이때 이 문제를 해결하는 도구가 npx이다. npx는 일회성으로 원하는 패키지를 npm 레지에 접근해서 설치하고 실행시키기 때문에 자신이 따로 패키지를 설치하고 업데이트하는 과정이 없이도 npm 레지에 올라가있는 최신 버전을 실행시키면 되는 간편한 도구인 것이다.

간단하게 요약하자면...  
<span style="color: skyblue">npm</span>: <span style="color: #95a5a6">프로그램 및 패키지를 설치하는 프로그램</span> 인 것이고,  
<span style="color: skyblue">npx</span>: <span style="color: #95a5a6">프로그램을 임시로 설치해서 한번만 실행시키고 지우는 도구</span>인 것이다.  
이는 로컬 컴퓨터에서 공간을 낭비하지 않고, 가장 최신의 프로그램을 사용할 수 있다는 장점이 있다.
```terminal
npm install -g create-react-app
(npm을 이용한 리액트 설치)
```
```terminal
npx create-react-app 폴더이름
(npx를 이용한 리액트 설치)
```

### npx 사용 이유
npm 이라는 무거운 패키지 안에는 자주 사용하지 않는 파일들이 로컬에 남는 것  
npx는 최신 버전에 해당하는 패키지를 설치 및 실행 시 이전 버전 패키지를 제거 해줌

## React 기초 내용

