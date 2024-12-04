# Element

- React의 element는 리액트 애플리케이션의 가장 작은 단위
- element는 화면에 표시할 내용을 기술하는객체로 HTML tag와 유사하다.
- element는 불변(immutable)이며,  한 번 생성되면 그 내용을 변경할 수 업다. 

```javascript
const element = <h1>Hello, world!</h1>;
```

이 element는 h1⁠ tag를 사용하여 “Hello, world” 라는 텍스트를 화면에 표기함

### 불변이란?

- 한번 생성된 element의 내용을 직접 변경할 수 없다는 의미

```javascript
⁠const element = <h1>Hello, world!</h1>;
```

이 element를 만약에 수정하고 싶다면, 기존의 element를 수정하는 것이 아닌

```javascript
const newElement = <h1>Hello, React!</h1>;
```

이렇게 새로운 element를 생성해서 변경해야 한다.

> 리액트는 이러한 불변성을 통해 성능 최적화를 수행, 리액트는 element가 변경되지 않는다는 가정을 바탕으로 변경된 부분만 효율적으로 업데이트할 수 있다.  
> 
> 1. **예측 가능성**: 불변 객체는 변경되지 않기 때문에, 코드의 동작을 예측하기 쉽습니다.
> 2. **성능 최적화**: 리액트는 불변 객체를 비교하여 변경된 부분만 업데이트할 수 있습니다.
> 3. **디버깅 용이성**: 불변 객체는 상태 추적과 디버깅을 더 쉽게 만듭니다

* * *

# Component

- React Component는 리액트 애플리케이션을 구성하는 더 큰 단위. Component는 여러 element를 포함할 수 있으며, 재사용 가능한 UI 조각을 정의한다
- 함수형 / 클래스형 Component로 나눌 수 있다.

## 함수형 Component

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

- 이 component는 name 이라는 props를 받아서, “Hello, \[name\]” 이라는 텍스트를 화면에 표시한다.

## 클래스형 Component

```javascript
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

- 클래스형은 ES6 클래스 문법을 사용하여 정의된다.
- 클래스형 component는 상태(state) 와 생명주기 메소드를 사용할 수 있다.

## 불변?

- Component는 element와 달리 불변이 아님
- 상태(state)와 속성(props)을 관리하고, 상태가 변경될 때 마다 UI를 업데이트할 수 있다.
- 상태(State) : Component 내에서 관리되는 동적인 데이터, Component 내에서 변경될 수 있고 상태가 변경되면 component는 다시 렌더링된다.
- 속성(props) : Component 에 전달되는 읽기 전용 데이터, 부모 component 에서 자식 component로 데이터를 전달할 때 사용되며 component는 props를 직접 변경할 수 없고 불변

# Element vs Component

> Element는 리액트 애플리케이션의 가장 작은 단위로 화면에 표시할 내용을 기술하는객체  
> Component는 여러 element를 포함할 수 있는 더 큰 단위로 재사용 가능한 UI 조각

## 상태를 이용한 함수형 예시

```javascript
import React, { useState } from 'react';

function Counter() {
  // useState 훅을 사용하여 상태를 정의합니다.
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>카운트 증가</button>
    </div>
  );
}
```

- counter component는 count 라는 state를 가지고 있고, useState를 통해 state를 업데이트
- 

## 상태를 사용한 클래스형 예시

```javascript
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <p>현재 카운트: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          카운트 증가
        </button>
      </div>
    );
  }
}
```

- 이 예시에서 this.setState는 React Component를 상속받은 클래스형 component에서 자동으로 제공됨
- state 객체를 통해 상태를 관리할 수 있다.