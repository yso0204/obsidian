# Mulit Page Application
 처음에 구현했던 페이지는 아래와 같다
 ![](https://i.imgur.com/BDnwLMO.png)

peghun.html 을 요청하면, 해당 html에 해당하는 웹 페이지가 화면에 나타나고 panda.html을 요청하면 해당 페이지가 화면에 나타났다.

이렇게 개발한 사이트를 사용자, 브라우저, 서버로 나타내면 아래와 같다.

![](https://i.imgur.com/nG4uGtZ.png)

이렇게 웹 서버가 모든 페이지를 가지고 있는 방식을 여러 개의 웹 페이지를 갖는 애플리케이션 **Multi Page Application** 이라고 한다. 

또한, 웹서버에서 미리 html 파일들을 가지고 있는 상태에서 브라우저의 요청에 따라 알맞은 페이지를 전달해 렌더링 하는 방식을 **Server Side Rendering(SSR)** 이라고한다.

이러한 MPA는 많은 사이트들이 사용하고 있는 전통적인 방식이지만, 새로고침하듯 페이지가 바뀌고, 페이지간 이동이 느린 등의 문제가 있다.

# Single page Application
