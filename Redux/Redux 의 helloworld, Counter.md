# 전통적인 Redux 구조란?

초기 redux는 **flux 아키텍쳐** 의 영향을 받아 구조가 아주 뚜렷한데, 아래와 같은 구성으로 되어 있다.
1. Store : 상태(state)를 보관하는 창고
2. Actions : 어떤 일이 일어 났는지 설명하는 객체
3. Reducers : action을 기반으로 state를 어떻게 바꿀지 정의
4. Dispatch : action을 store에 보내는 함수
5. View(react) : state를 보여주고, 사용자 입력으로 action을 발생

# 구조 흐름도
User input -> dispatch(action) -> reducer(state 변경) -> store(state 저장) -> view(rerender)

- 상태는 store에 보관
- view -> dispatch -> action 발생
- reducer가 action을 보고 state 업데이트
- store 변경 -> view가 업데이트 된다.


# store.js
```js
import { createStore } from 'redux';
import { counterReducer } from './reducers';

export const store = createStore(counterReducer);
```

## 왜 중앙 상태 창고가 필요한가?
중앙 창고에서 상태를 관리하면, 
- 앱 전체에서 '현재 상태가 뭔지' 한 군데서 확인이 가능
- 어떤 컴포넌트든 동일한 상태에 접근 가능
- 상태 변경 흐름이 예측 가능 -> 문제 발생 시 추적이 가능

그냥 컴포넌트에서 `useState`를 쓰면 안되나?
- 작은 앱에서는 이게 더 낫지만, 컴포넌트의 뎁스가 깊어지면, 부모 자식 간의 주고받는 횟수가 많아지고, 추적이 어려워짐
- **전역 상태** 가 필요할 때는 Redux가 유리하다.
# action.js
```js
export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';

export const increment = () => ({
    type: INCREMENT
});

export const decrement = () => ({
    type: DECREMENT
});
```
- 액션은 객체이고, `type` 필드는 필수

## action은 왜 객체로 상태 변경을 요청 하는가?
> 상태 변경을 설명하는 것은 "무슨 일이 일어 났는지"를 말해주는 것

`{type : 'INCREMENT'}` 
이것만 보더라도, 카운터를 증가시키는 요청임을 알 수 있다.
- action은 기록으로 남길 수 있다.
- action log를 찍으면 언제 무슨 일이 있었는지 다 확인 가능하다.

함수 호출보다 더 '명확하게 기록'되는 구조
# reducers.js
```js
import { INCREMENT, DECREMENT } from "./action";

const initialState = {
    count: 0
};

export const counterReducer = (state = initialState, action) => {
    switch (action.type) {
        case INCREMENT:
            return {
                ...state,
                count: state.count + 1
            };
        case DECREMENT:
            return {
                ...state,
                count: state.count - 1
            };
        default:
            return state;
    }
};

```
- reducer는 **순수 함수**여야하고, **새로운 state 객체를 반환**해야한다.

# index.js
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { store } from './redux/store';
import { Provider } from 'react-redux';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```
- `Provider` 는 Contex API를 이용해 store를 React 앱에 제공


# app.js
```js
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "./redux/action";

function App() {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <div style={{textAlign:'center',marginTop:'50px'}}>
      <h1>Counter: {count}</h1>
      <button onClick={() => dispatch(increment())} >Increment</button>
      <button onClick={() => dispatch(decrement())} >Decrement</button>
    </div>
  )
}

export default App;
```
- view 역할을 한다. 현재 카운트와 버튼 2개로 + - 를 제공

