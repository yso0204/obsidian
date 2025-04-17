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
