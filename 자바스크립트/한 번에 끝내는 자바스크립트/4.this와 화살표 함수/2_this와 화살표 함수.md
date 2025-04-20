# 콜백 함수
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

콜백함수는 일반 함수 처럼 호출되기 때문이다.

## 화살표 함수 사용 시
```js
function Counter() {
    this.count = 0;
    setInterval( () => {
        this.count++;
        console.log(this.count);
    },2000)
}
const counter = new Counter();
```
정상적으로 2초마다 1씩 늘어난 count를 볼 수 있다.

화살표 함수의 this는 함수의 선언 위치의 상위 스코프를 보기 때문이다.

 함수의 선언 위치에 의해 스코프가 결정되는 것을 렉시컬 스코프라고 한다.
# 메서드

```js
const cafe = {
    brand: '이디야',
    menu: '아메리카노',
    print: () => {
        console.log(this);
    },
};

cafe.print();
```
![](https://i.imgur.com/KXLXb1n.png)

일반 함수로 선언했을 때 와는 다르게 `this`에  `window`가 바인딩 되어 출력된다.

일반 함수로 선언했을 때는 `cafe.print()`로 호출