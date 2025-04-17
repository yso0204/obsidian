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

