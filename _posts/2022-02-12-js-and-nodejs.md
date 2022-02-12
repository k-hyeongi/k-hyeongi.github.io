---
title: JavaScript and Node.js
date: 2022-02-13 00:30:00 +/-TTTT
categories: [Web, Javascript]
tags: [javascript, nodejs, frontend]
---
## 프로그래밍 언어란 무엇인가
> 프로그래밍 언어는 말 그대로 언어의 일종이다. 내가 영어라는 언어를 배우는 이유가 미국인과 대화하고 싶어서 인 것처럼 컴퓨터와 대화를 하고 싶어서 배우는 게 프로그래밍 언어이다.   
즉, <span style="color:skyblue; font-weight:bold">사람과 컴퓨터가 서로 의사소통을 할 수 있게 해주는 수단이자 도구인 것이다.</span>  

<br>

###  Q. 왜 프로그래밍 언어는 여러 개일까
> 그건 나와 같이 개발을 배우는 학부생의 입장에서는 별로 중요하지 않다. 간략하게 기업들은 본인들이 컨트롤할 수 없는 외부의 언어보다 본인들이 컨트롤할 수 있는 언어를 선호한다.  
결론은 <span style="color:skyblue; font-weight:bold">내가 만들고 싶은 제품(Ex. ios, android)을 서비스하는 플랫폼(Ex. apple, google)이 권장하는 프로그래밍 언어를 배우면 된다.</span>  

<br>

## JavaScript란?
> javascript는 일반적인 정의로는 <span style="color:skyblue">정적인 HTML페이지를 동적으로 움직이게 만들어주기 위해서 만들어진 프로그래밍 언어</span>이다.  
그러나 js는 순수하게 언어의 관점에서는 좋지 않은데 왜 자바스크립트는 좋은 언어가 아닐까?  

<br>

## JavaScript가 좋은 언어가 아닌 이유!
1. 더하기(+)와 빼기(-) 연산의 동작 방식  
숫자를 더하기(+) -> 덧셈 (13 + 3 = 16)  
문자를 더하기(+) -> 문자열 연결 ("13" + "3" = "133")  
숫자를 빼기(-) -> 뺄셈 (13 - 3 = 10)  
문자를 빼기(-) -> 뺄셈 ("13" - "3" = 10) <span style="color:red">????</span>

2. == 연산자의 동작 방식  
1 == 1 -> true  
1 == "1" -> true  
true == true -> true  
true == "true" -> false <span style="color:red">????</span>  
0 == [] -> true  
“0” == [] -> false  
0 == [0] -> true  
“0” == [“0”] -> true <span style="color:red">????</span>  

따라서 <span style="color:skyblue">자바스크립트에서는 웬만하면 등호 세개(===)로 비교해야 한다. 이렇게 비교하면 거의 다 맞게 작동하는 걸 볼 수 있다.</span>  
자바스크립트는 단 열흘만에 급조하여 완성된 프로그래밍 언어기 때문에 프로그래밍 완성도의 측면에서 그렇게 좋은 언어라고 볼 수 없겠다.

### Q1. JavaScript는 Java와 어떤 관련이 있는가
> 아무 관련이 없다. 자바의 인기에 편승하려고 자바스크립트라는 이름을 채택했다고 한다.

### Q2. JavaScript를 안 쓰고 HTML과 CSS 만으로 웹 프론트엔드를 만들 수 있는가
> 가능하고 권장할 때도 있다. 비개발자들과 웹사이트를 만들고 유지보수 시 자바스크립트는 사용하기에 적합하지 않다. 자바스크립트는 HTML, CSS와는 다르게 비개발자들이 이해하고 수정하기 어렵기 떄문에 개발자들만 고생한다.  

<br>

## Node.js란?
> 크롬 V8 엔진을 기반으로 하는 JavaScript 런타임  
초심자들은 이해하기 어려운 개념이기 때문에 <span style="color:skyblue; font-weight:bold">JavaScript로 백엔드, 즉 서버를 만들 수 있는 툴</span> 정도로 이해하면 된다.  

### Node.js의 성공 이유
1. 프론트엔드 엔지니어들의 지지가 매우 높았다.
2. Node.js의 공식 언어가 JavaScript였기 때문이다.  

## Node.js의 장점
> Django나 Spring과 비교해서 왜 Node.js를 쓸까 -> JavaScript를 사용해서  
<span style="color:skyblue; font-weight:bold">웹 프레임워크의 최신 트렌드를 전부 받아들이고 빨리 적용하면서 컴파일러 언어인 자바에 비해 코딩하기 더 쉽고 훨씬 대중적이며, php보다는 잘 만든 언어이고 JavaScript를 도입했다는 점.</span>

<br>

--------------------------------
## 참고한 영상
`데이터 유치원` 채널의 **`알쓸코잡`** 재생목록  
https://youtube.com/playlist?list=PLOTd4L3rH1qXZViF3k6n7BTfyhrJSvfTK
<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PLOTd4L3rH1qXZViF3k6n7BTfyhrJSvfTK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
