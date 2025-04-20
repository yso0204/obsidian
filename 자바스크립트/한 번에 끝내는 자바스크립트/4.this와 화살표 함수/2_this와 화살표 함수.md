
```js
function Counter() {
    this.count = 0;
    setInterval(function () {
        this.count++;
        console.log(count);
    },2000)
}
const counter = new Counter();
```

`setInterval`에 전달된 callback 함수의 `this`는 생성자 함수로 통해 생성된 `Counter()` 객체가 아닌 `window` 객체를 가리켜서 NaN이 2초마다 출력된다.



