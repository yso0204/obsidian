`...spread` `...rest` 같은 `...` 이지만 완전히 다르게 사용되고 구조 분해 할당과 밀접하게 연결된다.
# Spread
> 직역하면 확산, 전파 라는 뜻
> 실제 특성 배열의 요소나 객체의 프로퍼티 값들을 펼치는 역할

## 객체
```js
const toy = {
    type: "bear",
    price: 15000,
};
const blueToy = {
    type: "bear",
    price: 15000,
    color: "blue",
};

const yellowToy = {
    type: "bear",
    price: 15000,
    color: "yellow",
};
```

Toy의 성질들이 겹치는데?

```js
const toy = {
    type: "bear",
    price: 15000,
};

const blueToy = {
    ...toy,
    color: "blue",
};

const yellowToy = {
    ...toy,
    color: "yellow",
};

console.log(blueToy);
console.log(yellowToy);
```

이렇게 spread는 `...` 을 사용해 특정 객체가 가진 프로퍼티를 펼쳐서 사용이 가능하다.
## 배열
```js
const color1 = ["red", "orange", "yellow"];
const color2 = ["blue", "navy", "purple"];

const rainbow = [...color1, "green", ...color2];

console.log(rainbow);

[
  'red',    'orange',
  'yellow', 'green',
  'blue',   'navy',
  'purple'
]
```

마찬가지로 배열에서도 사용이 가능함

# rest
> 나머지 매개변수라고도 부르며, `...`을 이용하기에 spread와 비슷해 보이지만, rest는 이와 반대로 하나의 배열이나 객체로 묶는 문법이다.

## 객체
```js
const blueToy = {
    type: "bear",
    price: 15000,
    color: "blue",
};

const { type, ...rest } = blueToy;

console.log(type);
console.log(rest);

bear
{ price: 15000, color: 'blue' }
```

type을 제외한 나머지 값들이 rest 라는 객체에 들어간 것을 볼 수 있다.

하지만, spread와는 다르게 순서에 상관이 있고, 항상 맨 마지막에 사용해야한다.
`const { ...rest, type } = blueToy;`
이렇게 사용하면 
`SyntaxError: Rest element must be last element`
에러가 발생

## 배열
```js
const color = ["red", "orange", "yellow", "green"];
const [c1, c2, ...rest] = color;

console.log(c1);
console.log(c2);
console.log(rest);

red
orange
[ 'yellow', 'green' ]
```
rest에 나머지 값들이 할당된 것을 알 수 있다.

## 함수
