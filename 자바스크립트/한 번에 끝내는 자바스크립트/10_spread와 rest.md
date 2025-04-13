`...spread` `...rest` 
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

