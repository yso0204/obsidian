
> [https://m.blog.naver.com/magnking/220972680805](https://m.blog.naver.com/magnking/220972680805)  

## BOM이란?

웹 서비스 개발은 브라우저와 밀접한 관련이 있음

모든 서비스는 웹 브라우저를 바탕으로 실행되고, 이 브라우저와 관련된 객체들의 집합을 브라우저 객체 모델(Browser Object Model) 이라고 부름

이 BOM을 이용하여 Browser와 관련된 기능들을 구성하는데 DOM은 BOM 중 하나임

  

BOM의 최상위 객체는 window 라는 객체, DOM은 window 객체의 하위 객체 이기도 함

  

## DOM이란?

DOM(Document Object Model) 즉 문서 객체 모델

### 문서 객체란?

<html> 이나 <body> 같은 html 문서들의 태그를 JavaScript가 이용할 수 있는 객체(object)로  만들면 이것을 문서 객체라고 한다.

### 모델?

model이라는 뜻은 모듈이라는 의미도 있는데, 여기서는 문서 객체를 ‘인식’ 하는 방식

  

즉 DOM은 웹브라우저가 HTML 페이지를 인식하는 방식을 의미하며, 문서객체와 관련된 객체의 집합

  

### DOM의 모형

![[Pasted image 20241204225649.png]]

DOM은 tree 형식의 자료구조를 가지고 있음

![[Pasted image 20241204225706.png]]

DOM 에 포함된 <p> 태그를 뜯어보면, 자식노드와 속성을 tree 구조로 가지고 있음을 알 수 있음

  

### node 란?

tree 구조에서 root node를 포함한 모든 개체

html tag 뿐 아니라 텍스트, 속성 도 모두 node 이며, 이 중에서 HTML tag 를 요소노드(element node) ,  요소 노드 내부 글자를 text 노드라 부르기도 함

  