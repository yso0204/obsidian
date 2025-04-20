지금까지 js에서 `this`는 함수 호출 방식에 따라 자동으로 결정된다는 알았지만, 다른 언어들에서 처럼 `this`를 그냥 해당 class나 객체에서 지정해서 사용하길 원할 때가 있다.

아래와 같은 방법으로 `this`를 강제로 할당할 수 있다.

# 예시
```js
const cafe = {
  brand: '스타벅스',
};

function printMenu(menu, size) {
  console.log(`${this.brand}의 ${menu} (${size})`);
}
```