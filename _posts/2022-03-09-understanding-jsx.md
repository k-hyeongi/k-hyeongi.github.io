---
title: React - JSX 알아보기
date: 2022-03-09 22:00:00 +/-TTTT
categories: [Web, React]
tags: [web, frontend, reactjs, jsx]     # TAG names should always be lowercase
image:
  src: /assets/img/understanding-jsx/react-jsx.webp
  width: 800
  height: 500
---

# 요약
근본적으로 JSX 파일은 React.createElement (component, props, … , children)에 대한 문법적 설탕을 제공하는 것 그 이상도 그 이하도 아니다.  

**HTML**
```html
<MyButton color=“blue” shadowSize={2}>
	Click Me
</MyButton>
```
이 HTML파일을 JSX파일로 컴파일

**JSX**
```jsx
React.createElement(
	MyButton,
	{color: ‘blue’, shadowSize: 2},
	’Click Me’
)
```
HTML을 JSX로 컴파일하는 또다른 예시
HTML
```html
<div className=“sidebar” />
```
JSX
```jsx
React.createElement(
	‘div’,
	{className: ‘sidebar’}
)
```  

# React 엘리먼트 타입 지정
JSX 형식 태그의 첫부분은 React Element의 타입을 결정한다.
**React가 반드시 Scope 내에 존재해야 한다**  
React library도 JSX 코드와 같은 scope 안에 있어야 한다.  
> React는 JavaScript 코드에선 직접적으로 사용되지는 않지만 JSX 태그로 사용할 수 있기 위해 반드시 import 해야 한다.
`import React from ‘react’;`

## JSX 타입을 위한 점 표기법
JSX 내에서도 점 표기법을 사용해서 React 컴포넌트를 참조한다. 이 방법은 하나의 모듈에서 복수의 React 컴포넌트들을 export 하는 경우에 편리하게 사용할 수 있다.
```jsx
import React from ‘react’;

const MyComponents = {
	DatePicker: function DatePicker(props) {
		return <div>Imagine a {props.color} datepicker here.</div>;
	}
}

function BlueDatePicker() {
	return <MyComponents.DatePicker color: “blue” />
}
```
위 예시에선 MyComponents의 DatePicker를 점 표기법을 사용해서 호출한 것을 확인할 수 있다.

## 사용자정의 컴포넌트는 반드시 대문자 시작
- Element가 소문자로 시작하는 경우는 `<div>`, `<span>`과 같은 내장 컴포넌트들일 경우이다.  
=> 이는 ‘div’, ‘span’처럼 문자열형으로 React.createElement에 전달된다.
- Element가 대문자로 시작하는 경우는 `<Foo />`와 같은 사용자 정의 컴포넌트이다.  
(사용자정의 컴포넌트란 JavaScript 파일 내에 사용자가 정의했거나, import한 컴포넌트를 말한다.)
=> React.createElement(Foo)와 같은 형태로 컴파일 된다.

```jsx
import React from 'react';

// 올바른 표기 방법이다. 아래는 사용자 정의 컴포넌트이므로 대문자로 시작한다.
function Hello (props) {
	// 올바른 사용법이다. 아래 <div>태그는 유효한 HTML 태그이기 때문에 유효하다.
	return <div>Hello {props.toWhat}</div>;
}

function HelloWorld() {
	// 올바른 사용법이다. React는 <Hello />가 대문자로 시작하므로 사용자정의 컴포넌트로 인식한다.
	return <Hello toWhat="World" />;
}
```

## 실행 중 타입 선택하기 
React Element에 일반적인 표현식은 사용할 수 없다.
```jsx
import React from 'react';
import { PhotoStory, VideoStory } from './stories';

const components = {
	photo: PhotoStory,
	video: VideoStory,
};

function Story (props) {
	// 잘못된 표현이다. JSX 타입을 직접적이게 표현식으로 사용 불가하다.
	// return <components[props.storyType] story={props.story} />;
	
	// 올바른 표현. 대문자로 시작하는 변수만 JSX타입으로 가능하다.
	const SpecificStory = components[props.storyType];
	return <SpecificStory story={props.story} />;
}
```

# JSX 에서 props 사용하기
## 1. JavaScript 표현식
JavaScript 표현식을 { }(중괄호) 안에 넣어서 props 으로 사용한다.  
if 구문과 for loop 등은 JavaScript 표현식의 범위 안에 들어가지 않기 때문에 JSX 안에서 직접적으로는 사용할 수 없다. 따라서, 아래 코드처럼 바깥쪽에 간접적으로 사용해야 한다.
```jsx
function NumberDescriber (props) {
	let description;
	if (props.number % 2 === 0) {
		description = <strong>even</strong>;
	} else {
		description = <i>odd</i>;
	}
	return <div>{props.number} is an {description} number</div>;
}
```
### JavaScript 표현식의 범위
그렇다면 JSX에서 props로 사용할 수 있다는 자바스크립트 표현식의 범위는 어디까지일까?  

먼저 표현식이란 무엇일까. <span style="color:skyblue">표현식(expression)은 값으로 평가될 수 있는 임의의 유효한 코드 단위 즉, 문(statement)이다.</span>  
표현식이 평가되면 새로운 값을 생성하거나 기존 값을 참조한다는 것이다.  
<span style="color:skyblue">이때의 값(value)이란, 표현식(expression)이 평가(evaluate)되어 생성 되어진 결과를 의미하는데 평가(evaluate)는 표현식을 해석해서 값을 생성하거나 참조하는 것을 나타낸다.</span>  

결국, 값으로 평가될 수 있는 모든 statement들은 표현식이라고 볼 수 있다.
```js
// 리터럴 표현식
0721
'Hello World!'

// 식별자 표현식 (선언은 이미 존재하는 경우)
sum
person.age
arr[0]

// 연산자 표현식
20 + 30
sum = 21
sum !== 20

// 함수/메소드 호출 표현식 (선언은 이미 존재하는 경우)
person.getAge()
square()
```
## 2. 문자열 리터럴
문자열 리터럴을 props로 넘겨서 줄 수 있다. 아래의 두 JSX 표현은 동일한 결과를 도출한다.
```jsx
<MyComponent message="Hello, World!" /> // 문자열 리터럴로
<MyComponent message={'Hello, World!'} /> // JavaScript 표현식으로
```
## 3. props의 default는 "True"
props에 어떠한 값도 할당하지 않는 경우, default 값은 `true`이다. 아래의 두 JSX 표현은 동일하다.
```jsx
<MyTextBox autocomplete />
<MyTextBox autocomplete={true} />
```
<span style="color:skyblue">React 공식문서에서는 props에 값을 전달하지 않는 것을 권장하지 않는다.</span>  
이는 `JavaScript의 객체 초기자`와 헷갈릴 수도 있기 때문이라고 한다.  
Ex) JSX에서 `{foo}`는 `{foo: true}`가 아닌 `{foo: foo}`로 동작한다. 

# JSX에서 자식(children) 다루기
## 문자열 리터럴
여는 태그와 닫는 태그 사이에 문자열 리터럴을 넣을 수 있고, 이 때 `props.children`은 그 문자열이 된다.
```jsx
<MyComponent>Hello World!</MyComponent>
```
여기서 `MyComponent`의 `props.children`은 `Hello World!` 이다.  
<span style="color:skyblue">일반적으로 HTML을 쓰는 방식으로 JSX를 그대로 쓸 수 있다.</span>
## JSX
JSX element 역시 자식으로 사용할 수 있다. 이는 중첩된 Component를 보여줄 때 유용하다.  
```jsx
<MyContainer>
	<MyFirstChildren />
	<MySecondChildren />
</MyContainer>
```
다양한 타입의 자식들을 혼합해서 사용할 수도 있기 때문에 문자열 리터럴을 JSX 자식과 함께 사용할 수 있다.   

<span style="color:skyblue">React Component에서는 element로 이루어진 배열을 return 할 수도 있다.</span>
```jsx
render() {
	// 리스트 item들을 굳이 추가적인 element로 감쌀 필요 없다
	return [
		// jsx에서 리스트 사용시 반드시 key 지정하기
		<li key="A">First item</li>,
		<li key="B">Second item</li>,
		<li key="C">Third item</li>,
	];
}
```
## JavaScript 표현식
{ }(중괄호)를 통해서 JavaScript 표현식 역시 자식으로 사용할 수 있다. 아래 두 코드들은 동일하다.
```jsx
<MyComponent>foo</MyComponent>
<MyComponent>{'foo'}</MyComponent>
```
<span style="color:skyblue">JavaScript 표현식을 자식으로 사용하는 방법은 임의 길이의 JSX 표현식의 배열을 렌더링할 때 유용하게 사용된다. 아래 코드는 HTML 배열(`<li>`)로 렌더된다.</span>
```jsx
function Item(props) {
  return <li>{props.message}</li>;}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}    </ul>
  );
}
```
## 함수(Function)
함수를 자식으로 사용할 수 있다.  
<span style="color:skyblue">`props.children`은 다른 props들처럼 React가 렌더링 할 수 있는 데이터의 형태 이외에도 어떤 형태의 데이터를 넘겨 받을 수 있다. 사용자정의 컴포넌트가 있다면 `props.children`을 통해서 콜백 받을 수 있다.</span>
```jsx
// 자식 콜백인 numTimes를 호출하여 반복되는 컴포넌트를 생성합니다.
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
	  items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```
이러한 사용법이 일반적이다고는 할 수 없지만, JSX 기능의 확장성을 보여주는 부분이다.
## boolean, null, undefined는 무시 
`true`, `false`, `null`, `undefined`는 모두 유효한 자식이나, 단지 렌더링 되지 않는다.  
이는 React element를 조건부 렌더링 시 유용하게 사용된다. 아래 코드는 `showHeader`가 `true`일 때 동일하게 `<Header />`를 렌더한다.
```jsx
<div>
  {showHeader && <Header />}  <Content />
</div>
```
반대로 `true`, `false`, `null`, `undefined`과 같은 값들을 출력하고 싶다면 먼저 문자열로 전환해야 한다. (`String(thing)`)
```jsx
<div>
  My JavaScript variable is {String(myVariable)}.
</div>
```

--------------------------------------------------------

React를 제대로 공부하려면 리액트 웹사이트 들어가서 공식 문서를 직접 읽어보면서 이해하는 것을 적극 추천한다.  
출처: [React 공식 문서](https://ko.reactjs.org/docs/jsx-in-depth.html) (https://ko.reactjs.org/docs/jsx-in-depth.html)