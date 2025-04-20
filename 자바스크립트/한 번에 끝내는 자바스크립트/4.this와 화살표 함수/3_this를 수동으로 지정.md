지금까지 js에서 `this`는 함수 호출 방식에 따라 자동으로 결정된다는 알았지만, 다른 언어들에서 처럼 `this`를 그냥 해당 class나 객체에서 지정해서 사용하길 원할 때가 있다.

아래와 같은 방법으로 `this`를 강제로 할당할 수 있다.

# 예시
```js
const cafe = {
    brand: '스타벅스',
};

function printMenu(menu, size) {
    console.log(this);
    console.log(`${this.brand}의 ${menu} (${size})`);
}

printMenu(cafe, '아메리카노', '톨');
```
![](https://i.imgur.com/0GqlIp8.png)


현재 `this`는 `window`를 가리키고 있어 해당 값들이 정의되지 않앗다.

# `call()`

> 지금 이 객체(this)로 함수 실행해 라고 지정

`함수.call(지정할 this, 인자1, 인자2, ...)`

```js
const cafe = {
    brand: '스타벅스',
};

function printMenu(menu, size) {
    console.log(this);
    console.log(`${this.brand}의 ${menu} (${size})`);
}

printMenu.call(cafe, '아메리카노', '톨');
```
![](https://i.imgur.com/9C4yvGX.png)

비슷한 것으로 `apply()`가 있다.
# `apply()`
> `call()` 과 비슷하지만, 인자를 배열로 준다.

`함수.apply(지정할 this, [인자1, 인자2, ...])`
`printMenu.apply(cafe, ['카페라떼', '그란데']);` 로 실행
![](https://i.imgur.com/LwQ0wh8.png)


- `call()` 과 `apply()` 는 즉시 실행하는 특성이 있다.
# bind
> 이 객체(this) 와 묶은 함수를 새로 만들지만, call이나 apply 처럼 즉시 실행하는 것이 아님

`const 새함수 = 원본함수.bind(지정할 this, 인자....)`

- this와 인자를 미리 고정한 새 함수를 리턴만 하고 실행은 따로 해야한다.

```js
```