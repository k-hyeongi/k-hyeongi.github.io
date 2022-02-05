---
title: 마크다운 markdown에 대해서 알아보자
date: 2022-02-05 20:25:30 +/-TTTT
categories: [GitHub, Pages]
tags: [blog, markdown]     # TAG names should always be lowercase
image:
  src: assets/img/aboutMd/mdLogo.png
  width: 800
  height: 500
---
# 마크다운 Markdown
  

## 1. 마크다운이란?

>마크다운(Markdown)은 일반 텍스트 기반의 경량 마크업 언어이다. 마크업 언어란, 태그 등을 이용하여 문서나 데이터의 구조 등을 명기하는 언어의 한 가지이다. 텍스트만으로 서식이 있는 문서들을 작성할 때 자주 사용되며, 다른 마크업 언어들에 비해 문법이 쉽고 간단한 것이 특징. HTML 등의 서식 문서들로 쉽게 변환되기 때문에 README 파일이나 온라인 게시물 등에 사용된다.

## 2. 마크다운의 장단점

### 2-1. 장점
```
- 문법이 간결하고 쉽다.
- 거의 대부분의 것에 사용할 수 있다. (웹사이트, 문서, 메모, README 기술파일 등)
- 마크다운을 지원하는 플랫폼이 다양하다. (Github, Notion, Discord, Dropbox Paper 등)
- 대부분의 환경에서 작성 및 수정이 가능하다. (일반 Notepad에서도 가능)
- 텍스트로 저장되어 용량을 많이 차지하지 않는다.
- 다양한 형태로 변환이 가능하다.
```
### 2-2. 단점
```
- 모든 HTML의 마크업을 대신하지 못한다.
- 표준이 없기 때문에 툴에 따라 생성물이 다르다.
- 마크다운으로 파일을 업로드할 때 저장 이후 파일 경로를 입력해야 한다.
```
## 3. 마크다운의 문법 
> 다양한 플랫폼에서 사용하는 마크다운이기에 한 번 문법을 알아두면 뽕을 뽑을 수 있다.

------

## 3-1. Header

`h1 ~ h6`

```
# 안녕 나는 Header 1야
## 안녕 나는 Header 2야
### 안녕 나는 Header 3야
#### 안녕 나는 Header 4야
##### 안녕 나는 Header 5야
###### 안녕 나는 Header 6야
```
![Alt](/assets/img/aboutMd/header.png)

------

## 3-2. Styling
`Emphasize`
```
*Emphasize* or _emphasize_
```
*Emphasize* or _emphasize_

------

==String (Bold)==
```
**Strong** or __strong__
```
**Strong** or __strong__

------

`Highlight`
```
==Highlight things==
```
==Highlight things==  
</br>
<span style="color:red">하이라이팅은 여기선 안되나 보다. 마크다운의 단점.</span>

------

`Cancellation Line`
```
~~Cancellation Line~~
```
~~Cancellation Line~~

------

`Quoted Line`
```
> Quoted Line
```
> Quoted Line

------

`Chemical Formula`
```
H~2~O is a liquid.
```
H~2~O is a liquid.

------

`Mathematical Formula`
```
2^10^ is 1024.
```
2^10^ is 1024.  
</br>
<span style="color: orange">화학식과 수식을 나타내는 문법도 여기선 표현이 안되는 것을 알 수 있다.</span>

------

## 3-3. List
```
- item
	* item
		+ item
-, *, + 중 어떤 걸로 사용하던 상관없음.
```
- item
	- item
		- item

------
```
- [ ] Incomplete item
- [x] Complete item
```
- [ ] Incomplete item
- [x] Complete item

------

## 3-4. Link
```
[NAVER](https://naver.com)
Eagle ![Alt](https://images.unsplash.com/photo-1643114673614-55af01ec8dfc?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHx0b3BpYy1mZWVkfDM2fDZzTVZqVExTa2VRfHxlbnwwfHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60)
```
[NAVER](https://naver.com)
Eagle![Alt](/assets/img/aboutMd/eagle.jpeg)

------

## 3-5. Code
```
Some `inline code`
```
Some `inline code`

------
==By using three `==
```
// using ```
var md = 'markdown';
```
------
==By using three ` & prog lang==
```c
// using ```c
int main() {
	printf("Hello, World");
}
```
------
## 3-6. Table
```
Item	 | Value
------	 | -----
아메리카노	 | ₩2500
코카콜라	 | ₩1200
국밥		 | ₩6000
```
Item	 | Value
------	 | -----
아메리카노	 | ₩2500
코카콜라	 | ₩1200
국밥		 | ₩6000

------

```
| Column 1 | Column 2 	   |
|:--------:| -------------:|
| centered | right-aligned |
```
| Column 1 | Column 2 	   |
|:--------:| -------------:|
| centered | right-aligned |  
</br>
<span style="color:green">원래 표가 생성되야 하는 게 맞는데 안된다...</span>


------

## 3-7. Definition List
```
Handong University
: 경상북도 포항시 북구 흥해읍에 위치한 개신교계 사립 대학교
Majors
: 전산전자공학부
: 기계제어공학부
: ICT창업학부 
: ETC.
```
Handong University
: 경상북도 포항시 북구 흥해읍에 위치한 개신교계 사립 대학교

Majors
: 전산전자공학부
: 기계제어공학부
: ICT창업학부 
: etc.

------

## 3-8. Footnote
```
Some text with a footnote.[^1]
[^1]: The footnote.
```
Some text with a footnote.[^1]
[^1]: The footnote.
------
## 3-9. Abbreviation
```
Markdown converts text to HTML.
*[HTML]: HyperText Markup Language
```
Markdown converts text to HTML.
*[HTML]: HyperText Markup Language
------
## 3-10. LaTeX math
```
The Gamma function satisfying $\Gamma(n) = (n-1)!\quad\forall
n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$
```
The Gamma function satisfying $\Gamma(n) = (n-1)!\quad\forall
n\in\mathbb N$ is via the Euler integral

$$
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
$$

