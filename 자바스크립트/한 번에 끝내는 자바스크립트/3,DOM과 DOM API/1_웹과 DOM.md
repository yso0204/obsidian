# DOM이란?
> DOM 이란 Document Object Model 로 문서 객체 모델이다.
>

# 웹의 구성 요소
![](https://i.imgur.com/8UPzGOx.png)
> 최상단에는 `window`라 불리는 루트 객체가 있다

1. 자바스크립트의 전역 객체로 전역 함수의 부모 처럼 작동한다
```js
var x = 10;
console.log(window.x); // 10
```
2. 브라우저 창(browser window)를 대변하고 이를 제어 할 수 있는 메서드를 제공
	- 말 그대로 실제 브라우저 창을 다룰 수 있는 기능들이 `window`에 담겨 있다는 뜻

| 기능        | 메서드                  | 설명             |
| --------- | -------------------- | -------------- |
| 새 창 열기    | window.open()        | 새 브라우저 창을 염    |
| 알림창       | window.alert()       | 경고창            |
| 스크룰 위치 이동 | window.scrollTo()    | 스크롤 위치 이동      |
| 현재 URL 확인 | window.location.href | 현재 주소창의 URL 리턴 |

- 이 외에도 다향한 메서드와 프로터티가 존재함
## DOM 과 DOM 트리
>  DOM은 HTML로 작성된 여러 요소들에 js 가 접근하고 조작할 수 있도록 브라우저가 변환시킨 객체이다.
>  브라우저는 HTML 문서를 불러온 다음, 요소간의 상하 관계를 한 눈에 볼 수 있도록 트리 구조로 나타내는데 이걸 DOM 트리라고 부른다

![](https://i.imgur.com/Gwr8YN8.png)
>오른쪽 DOM 트리는 HTML tag 요소들로 Node 라고 부르며 Node 들은 하나의 객체로 이루어져 있다.

