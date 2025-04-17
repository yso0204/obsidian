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

기존의 type요소에 text 값이 추가된 것이 아닌, 별도의 te