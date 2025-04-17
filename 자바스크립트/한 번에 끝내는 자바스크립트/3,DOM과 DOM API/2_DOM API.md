> js를 사용하여 DOM 요소에 접근하려면 DOM API를 사용하여 조작하고자 하는 요소의 최상단인 
> document에 접근하여, 요소 노드, 어트리뷰트 노트, 텍스트 노드를 순서대로 거쳐 접근한다.

![](https://i.imgur.com/KtDtdmt.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <title>DOM Tree</title>
        <meta charset="UTF-8" />
    </head>
    <body>
        <div class="animal-info">
            <div id="name">강아지</div>
            <div id="color">갈색</div>
            <div id="age">2살</div>
        </div>
        <script src="src/index.js"></script>
    </body>
</html>
```
HTML에서 요소를 작성할 때는 `class`와 `id`를 사용해 요소의 이름을 지정할 수 있는데, `class`는 보통 반복적으로 사용되는 css 스타일 같은 것을 지정할 때 주로 사용하고, header나 footer 같은 요소나 내부에 있는 세부적인 스타일을 적용할 때는 `id`를 사용한다.

## `document.getElementById()`
> 특정 요소를 id 값으로 가져온다는 의미로 실제로 특정 요소의 객체 값을 반환한다.

```js
let $color = document.getElementById("color");
console.log($color);
```
![](https://i.imgur.com/WYCvgYn.png)

id 값이 color 인 div 요소가 출력되었다.

## `document.querySelector()`
> 특정 요소의 id가 아닌 css 선택자로 요소 노드를 반환하는 API

```js
let $animalInfo = document.querySelector('div.animal-info');
let $age = document.querySelector('div#age');

console.log($animalInfo);
console.log($age);
```
tag를 쓰고, class를 찾으면 `.`을
id를 찾는다면 `#` 을 사용한다.
![](https://i.imgur.com/nBLvHOT.png)


위 2개 API는 단 하나의 요소만을 반환하지만, 조건을 만족하는 요소가 여러 개일 경우 해당 요소를 전부 반환하는 DOM AP도 있다.
`querySelectorAll`, `getElementsByClassName`, `getElementsByTagName` 가 대표적이다.

## `document.querySelectorAll()`
> 전달받은 class 이름을 가지고 있는 여러 요소들을 전부 반환

```html
<!DOCTYPE html>
<html>
    <head>
        <title>DOM Tree</title>
        <meta charset="UTF-8" />
    </head>
    <body>
        <div class="animal-info">
            <div class="info-item" id="name">강아지</div>
            <div class="info-item" id="color">갈색</div>
            <div class="info-item" id="age">2살</div>
        </div>
        <script src="src/index.js"></script>
    </body>
</html>
```

```js
let $infoItem = document.querySelectorAll('div.info-item');
console.log($infoItem);
```

![](https://i.imgur.com/e6PfUSo.png)

class 이름이 info-item 인 요소들이 nodeList에 담긴 것을 볼 수 있다.

## `document.getElementsByClassName()`
> class 이름만으로 여러 요소들을 찾는 API

```js
let $infoItem = document.getElementsByClassName('info-item')
console.log($infoItem);
```
![](https://i.imgur.com/iHFvs44.png)

HTMLCollection 안에 info-item class 들이 담겨있는 것을 볼 수 있다.
## `document.getElementsByTagName()`
> html의 `div`나 `img` 등과 같은 tag 이름을 통해 요소들을 찾는다

```js
let $div = document.getElementsByTagName("div");
console.log($div);
```
![](https://i.imgur.com/BPLNdVX.png)

`div` tag들이 HTMLCollection 에 담긴 것을 볼 수 있다.

요소들의 속성값과 텍스트 등을 변경할 수 있는 API들을 알아 보자
## `className`
> class 이름을 변경하는 API


![](https://i.imgur.com/kYXpO0i.png)

```js
let $name = document.getElementById('name');
$name.className = ('dog-name');
console.log($name);
console.log($name.className);
```

## `id`
```js
let $name = document.getElementById('name');
$name.className = ('dog-name');
console.log($name);
console.log($name.className);
$name.id = 'name2';
console.log($name);
console.log($name.id);
```
![](https://i.imgur.com/smdgLP5.png)


## `classList`
> `className`과 비슷하게 요소의 class 에 접근 가능하다

classList는 className 처럼 특정 요소의 class 속성에 접근 가능하지만 아래 사진과 같이 여러 메서드를 제공한다.
![](https://i.imgur.com/HZ7vFHH.png)

### className vs classList
> className은 요소 전체 클래스 이름을 문자열로
> classList는 요소 전체 클래스 목록을 배열처럼 다룬다

```js
let $color = document.getElementById('color');

console.log($color.className);
console.log($color.classList);
```

![](https://i.imgur.com/ysnBJ2d.png)

### method

#### `add()`
```js
let $color = document.getElementById('color');

$color.classList.add('dog-color')
console.log($color.classList);
```
![](https://i.imgur.com/xKjGyOS.png)

#### `remove()`
```js
let $color = document.getElementById('color');

$color.classList.add('dog-color')
console.log($color.classList);
$color.classList.remove('info-item')
console.log($color.classList);
```
![](https://i.imgur.com/myFK6A5.png)

#### `toggle()`
> 있으면 제거, 없으면 추가

```js
let $color = document.getElementById('color');

$color.classList.toggle('hidden')
console.log($color.classList);
$color.classList.toggle('hidden')
console.log($color.classList);
```
![](https://i.imgur.com/tKN2OvF.png)

## `textContent`
> 요소 노드의 텍스트 노드 값을 조작

```js
let $color = document.getElementById('color');

$color.textContent = 'blue'
```
![](https://i.imgur.com/9U6TPye.png)

## `style`
> 요소의 스타일을 추가하고 수정

```js
let $color = document.getElementById('color');
$color.style.color = 'blue';
$color.style.fontSize = '30px';

console.log($color);
```
![](https://i.imgur.com/UxTyL3f.png)
