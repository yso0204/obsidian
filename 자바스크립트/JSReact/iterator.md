# iterator
> 순차적으로 데이터를 하나씩 꺼낼 수 있는객체
> 배열, 문자열, Map, set 등이 iterable 이고
> for...of 같은 문법으로 순회 할 수 있는건 iterator를 구현하고 있기 때문이다.

## 기본개념
아래 두 가지 조건을 충족하는 객체
1. `next()` 메서드를 가지고 있다.
2. `next()`
를 호출하면 `{value: 값, doen: boolean}` 형태의 객체를 반환

`iterable` 객체는 반드시 `Symbol.iterator`라는 특별한 키를 가져야 한다.

