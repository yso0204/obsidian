> prototype은 공통된 기능을 공유하기 위한 설계도
> 자바스크립트에서 객체들이 공통된 기능을 가지게 하려면 `prototype`에 정의한다.

```js
function Person(name) {
    this.name = name;
}

Person.prototype.sayHello = function () {
    console.log(`안녕하세요 저는 ${this.name} 입니다.`)
}

let me = new Person('sam');
me.sayHello();

안녕하세요 저는 sam 입니다.
```

중요한 점은 `sayHello()`는 객체 `me` 에 직접 들어있는 것이 아니다.
`Peson.protype` 에 들어 있는걸, `me`가 **상속** 받아서 사용할 수 있는 것이다.

