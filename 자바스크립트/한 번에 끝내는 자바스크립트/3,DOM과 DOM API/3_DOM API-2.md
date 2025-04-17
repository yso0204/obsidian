새로운 요소를 추가하는 API들도 존재한다.

## `createElement()`
> 새로 생성할 요소의 `tag`를 전달

```js
let $type = document.createElement('tag');
$type.id = 'type';
$type.class = 'info-item';
$type.textContent = '말티즈';

console.log($type);
```
![](https://i.imgur.com/kdE2PI1.png)

## `createTextNode()`
> 위 코드처럼 textContent로 직접 넣어줘도 되지만
> `createTextNode()` 를 사용하여 텍스트 노드 객체를 생성할 수도 있다.

```js
let $type = document.createElement('div');
$type.className = 'info-item';
$type.id = 'type';
let $typeText = document.createTextNode('말티즈');

console.log($type);
console.log($typeText);
```
![](https://i.imgur.com/GUk7ag8.png)

기존의 type요소에 text 값이 추가된 것이 아닌, 별도의 text 노드가 생성이 된다.

텍스트 노드를 하나의 객체처럼 다룰 수 있는데 이는 복잡한 구조를 만들 때 유리하다

## `appendChild()`
> 전달받은 노드를 원하는 요소의 마지막 자식으로 추가할 수 있다.

![](https://i.imgur.com/tivT0Pp.png)

`$type` 요소 노드는 class 가 `animal-info` 요소 노드의 아래에 class가 `info-item` 이고 id가 `name`,`color`,`age`요소 노드들과 동등한 위치에 있어야 한다.

```js
let $type = document.createElement('div');
$type.className = 'info-item';
$type.id = 'type';
let $typeText = document.createTextNode('말티즈');

let $animalInfo = document.querySelector('div.animal-info');
$animalInfo.appendChild($type);
$type.appendChild($typeText);

```
![](https://i.imgur.com/gZob9RF.png)

부모 노드를 찾고, `.appendChild`로 차례로 자식 노드를 추가해준다.

## `addEventListener()`
> DOM의 특정 요소에 여러가지 이벤트를 추가 할 수 있다.

```js
let $button = document.createElement('button');
$button.id = 'new-button';
$button.classList.add('new-button');
$button.textContent = '버튼';
$button.addEventListener('click', () => {
    alert('click')
})
let $animalInfo = document.querySelector('div.animal-info');
$animalInfo.appendChild($button);
console.log($animalInfo);

```
![](https://i.imgur.com/cJDeic1.png)

이렇게 `click`,`scroll` 등등을 넣어서 이벤트를 넣어서 작성할 수 있다.

## `innerHTML`
> 특정 요소의 내부에 HTML 요소를 추가할 수 있다
> `innerHTML`은 특정 요소의 HTML을 문자열 형태로 읽거나 설정할 수 있다.

```js
let $animalInfo = document.querySelector('div.animal-info');
console.log($animalInfo.innerHTML);
```
![](https://i.imgur.com/Kgu9Qju.png)

이렇게 모든 HTML 요소들이 출력되는데 아래처럼 기존 HTML요소들을 날리고 새롭게 지정할 수 있다.
```js
let $animalInfo = document.querySelector('div.animal-info');
$animalInfo.innerHTML = '<div id="name">고양이</div>';
console.log($animalInfo.innerHTML);
```
![](https://i.imgur.com/RoeuPj1.png)

새로운 요소들을 쉽게 설정하고 변경할 수 있지만, 보안과 성능에 문제가 있기 때문에 가능하면 `createElement`나 `textContent`와 같은 API를 사용하는 것이 좋다.

보안과 성능을 위해 innerHTML보다는 createElement나 textContent 같은 안전한 API를 사용하고, 기존 내용을 제거하려면 removeChild나 innerHTML = ''로 직접 삭제한 후 추가하면 된다.

## xss 보안 문제 예시
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>XSS 실험</title>
</head>
<body>
  <input type="text" id="input-box" placeholder="이름을 입력하세요">
  <button onclick="greet()">인사하기</button>

  <div id="result"></div>

  <script src="script.js"></script>
</body>
</html>
```

```js
function greet() {
    const userInput = document.getElementById("input-box").value;
  
    // 보안 취약 코드
    document.getElementById("result").innerHTML = "안녕하세요, " + userInput + "님!";
  }
```

여기서 만약에 console에
```
document.getElementById("input-box").value = `<img src="x" onerror="alert('해킹!')">`;
```

라고 입력 후 버튼을 누르면

input box에 `<img ...` 이게 들어가고 브라우저가 그 문자열을 HTML로 해석해서 img 로딩 실패, onerror 트리거, alert을 실행하게 된다.

userinput 값이 HTML 태그로 해석되기에 문자열로 보여주는게 아니고 실제로 실행을 시키게 된다.

`document.getElementById("result").textContent = "안녕하세요, " + userInput + "님!";
`
이렇게 넣어야 저런게 들어와도 글자로만 보여준다.


