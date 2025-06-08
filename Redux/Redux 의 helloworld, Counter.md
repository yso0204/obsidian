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


# store
```js
import { createStore } from 'redux';
import { counterReducer } from './reducers';

export const store = createStore(counterReducer);
```

# action
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

# reducers
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
