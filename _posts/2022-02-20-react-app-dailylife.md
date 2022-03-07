---
title: React 웹앱 구현하기 (생활코딩)
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

## npm run start? build?

- 개발하는 중: `npm run start`  
➡️ localhost로 개발중인 리액트 웹앱을 실행해줌으로써 작업중인 내용을 테스트하고 확인하기 좋다. 그러나 `npm run start`의 단점은 웹의 용량이 상당하다는 점이다. (Default 기본 페이지의 크기가 약 2MB)
- 웹앱 완성 이후: `npm run build`  
➡️ 따라서 개발이 끝나고 완성한 후엔 `npm run build`를 통해서 build 폴더를 만들어주고, 그 build 폴더를 배포한다. 빌드된 웹의 용량은 상당히 개선된다. (Default 기본 페이지의 크기가 약 200KB)


## React 기초 내용

### **index.html, index.js**
맨 처음에 create-react-app을 통해서 리액트 프로젝트를 생성하게 되면 node_modules, public, src 폴더와 여러 json 파일들이 생성이 된다. 이 때 public 폴더에 index.html 파일이 있는 걸 볼 수 있을 것이다. 이 index.html 파일은 일종의 React Template으로 이 파일만 인터넷에서 열게 된다면 빈 화면만 나타나게 된다.  
index.html에서 중요한 부분은 body태그의 id="root" 부분이다.
```html
<body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
    <!--
        This HTML file is a template.
        If you open it directly in the browser, you will see an empty page.

        You can add webfonts, meta tags, or analytics to this file.
        The build step will place the bundled scripts into the <body> tag.

        To begin the development, run `npm start` or `yarn start`.
        To create a production bundle, use `npm run build` or `yarn build`.
    -->
</body>
```
저 부분에 React 프레임워크를 통해서 만들어진 태그들이 들어가 있다.
src 폴더 안의 index.js 파일에 보면
```jsx
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
ReactDOM이 render되는 부분이 있는데 여기서 index.html의 root 영역에 개입하는 것이다.  
```react
ReactDOM.render(element, container[, callback])
```
`React 엘리먼트를 container DOM에 렌더링하고 컴포넌트에 대한 참조를 반환합니다(무상태 컴포넌트는 null을 반환합니다).`

`React 엘리먼트가 이전에 container 내부에 렌더링 되었다면 해당 엘리먼트는 업데이트하고 최신의 React 엘리먼트를 반영하는 데 필요한 DOM만 변경합니다.`

`추가적인 콜백이 제공된다면 컴포넌트가 렌더링되거나 업데이트된 후 실행됩니다.`  

출처: 리액트 공식 사이트  

### **App.js**  
따라서 실제로 초기 웹앱을 구동했을 때 보여지는 화면은 App.js의 코드들인 것이다.
![리액트 기본화면](/assets/img/react-app-dailylife/initial_react.gif)

<center>리액트 초기설정 화면</center>

App.js의 이 부분이 보여진다.
```jsx
function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}
```
따라서 index.html 내 보여지는 부분을 수정하고 싶을 땐 App.js 내의
```jsx
<div className="App">
    ...
</div>
```
이 부분을 수정해주면 된다.  

### **Component**
```jsx
import React, { Component } from 'react'; // 필수

class App extends Component {
  render() {
    return (
      <div className="App">
        ...
      </div>
    );  
  }
}

export default App; // 필수
```
위 코드는 React의 Component 구조이다.  
- class 안에 소속된 함수는 function으로 시작하는 않고 생략해도 된다. 
- class는 반드시 render 메소드를 실행하고, 
- Component를 생성할 때 반드시 하나의 최상위 태그로 시작해야 한다.

이 구조가 모든 리액트 코딩의 근간이 된다.  
여기서 한 가지 신기했던 점은 위 코드들은 엄밀히 말하면 자바스크립트 코드가 아니다. 유사 자바스크립트 코드이고, 그렇기 때문에 위 코드를 크롬 콘솔에서 실행해보면 에러가 발생하는 것을 볼 수 있을 거다. 리액트에서 유사 자바스크립트 코드를 사용하는 이유는 무엇일까?  
페이스북에서 리액트를 개발할 때 자바스크립트에서 HTML 코드들을 사용하기 까다로워서 직접 JSX 형태를 개발해서 이 jsx파일을 리액트(create-react-app)를 통해서 js파일로 컨버팅 해준 것이다.  

<span style="color: skyblue">
리액트에서 Component의 생성은 정리정돈하는 것 정도로 생각하면 될 것 같다.
</span>

### **props & state**

처음에 props와 state에 대해서 들었을 때 이 둘의 차이에 대해서 되게 애매하게 느껴졌고, 거기서 거기라고 생각해서 개념 정리가 잘 안 됐던 것 같다. 그래서, 따로 props와 state에 대해서 포스팅할 예정이다. 일단 이 포스트에서는 크게 짚고 넘어가진 않겠다.  

state를 쓰기 위해서는 state를 쓸 class 안에
```jsx
  constructor(props) {
    super(props);
    this.state = {
      subject: {
        title: 'WEB',
        sub: 'World Wide Web!! 🤪',
      }
    }
  }
```
super(props)를 포함하는 constructor(props)가 필요하다.  

<span style="color: skyblue">
App이 내부적으로 사용할 요소들은 state를 사용해서 사용하지만  
index.js에서 바라볼때는 state를 사용하는지 모르게 하는 코드가 좋은 코드
</span>

### key
Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 도와준다.  
Key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 합니다.  

예시로 TOC.js 파일을 들 수 있다.
```jsx
import React, { Component } from 'react'

class TOC extends Component {
  ...

  render() {
    console.log("TOC is rendered...");
    let lists = [];
    let data = this.props.data;
    let i = 0;
    while(i < data.length) {
      lists.push(
      <li key={data[i].id}> // 이 부분이다.
        <a 
        href={"/content/" + data[i].id}
        data-id = {data[i].id}
        onClick={function(e) {
          e.preventDefault();
          this.props.onChangePage(e.target.dataset.id);
        }.bind(this)}
        >
        {data[i].title}
        </a>
      </li>);
      i += 1;
    }

    ...
  }
}

export default TOC;
```
위 코드에서 lists 배열 내부의 `<li>` 태그에 key를 지정한 것처럼 사용할 수 있다.  

그리고 위 코드에서 보이는 것과 같이 Key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것이다. 대부분의 경우 데이터의 ID를 key로 사용한다.

### 이벤트 생성
anchor를 클릭 시에 이벤트를 생성하게 할 것이다.  
예시로 위의 TOC.js와 아래 App.js 코드의 일부를 봐보자.
```jsx
  render() {  // class 안에 소속된 함수는 function을 생략한다.
    return ( // 하위 컴포넌트들
        <div className="App"> 

          ...

          <TOC 
            onChangePage={function(id) {
              this.setState({
                mode: 'read',
                selected_content_id: Number(id),
              })
            }.bind(this)}
            data={this.state.contents}>
          </TOC>
          
          ...

        </div>
    );
  }
```
JavaScript에서는 이벤트 처리시 문법이 `onclick=""` 이지만, React는 유사 JavaScript이므로 `onClick={}`을 사용한다.  
React에서는 `onClick={}`으로 이벤트를 처리하게 되면, 그 함수가 호출될 때, 그 함수의 첫째 매개변수 값으로 Event(e)라고 하는 객체가 주입되기로 약속되어 있다. (이벤트를 우리가 핸들링할 수 있도록 제공되는 것)  
이 e를 활용해서 많은 것을 할 수 있다.  

추가로 TOC.js 코드 중에 
```jsx
onClick={function(e) {
    e.preventDefault(); // 이 것.
    this.props.onChangePage(e.target.dataset.id);
}.bind(this)}
```
`e.preventDefault()`라는 메소드를 실행시키는 것을 볼 수 있는데 이 메소드는 e가 가리키는 이벤트가 발생한 태그의 기본적인 동작을 못하게 만드는 녀석이라고 보면 된다.  

그리고 추가로 위에 TOC.js에서 볼 수 있는 것처럼 bind(this) 메소드를 이벤트 처리 함수 뒤에 실행해줘야 한다. bind(this) 메소드를 실행해주지 않으면 이벤트를 실행했을 때 this가 누구를 가리키는지 찾을 수 없어서 에러가 발생하기 때문이다. 

#### bind() 메소드 이해하기

`console.log()`로 찍어서 확인해보면 render() 함수에서의 `this`는 class 자체를 가리킨다.  
그러나 `onClick={}` 이벤트 처리 중의 `this`는 `undefined`가 뜨는 것을 확인할 수 있다.  
왜 그런 것일까?  

JavaScript에서는 클래스 메서드는 기본적으로 바인딩되어 있지 않다.
onChangePage를 바인딩 하지 않고 onClick에 전달하였다면, 함수가 실제 호출될 때 this는 undefined된다.
이는 React만의 특수한 동작이 아니며, JavaScript에서 함수가 작동하는 방식의 일부이다.
일반적으로 onClick={this.handleClick} 과 같이 뒤에 ()를 사용하지 않고 메서드를 참조할 경우,
해당 메서드를 바인딩 해야한다.  

## 마치며

일단은 대충 여기까지 정리하는 것으로 하고, 다음 포스팅에서는 생활코딩에서 실습한 React로 하는 CRUD (Create, Read, Update, Delete)를 정리해보도록 하겠다.