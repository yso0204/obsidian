# 전통적인 Redux 구조란?

초기 redux는 **flux 아키텍쳐** 의 영향을 받아 구조가 아주 뚜렷한데, 아래와 같은 구성으로 되어 있다.
1. Store : 상태(state)를 보관하는 창고
2. Actions : 어떤 일이 일어 났는지 설명하는 객체
3. Reducers : action을 기반으로 state를 어떻게 바꿀지 정의
4. Dispatch : action을 store에 보내는 함수
5. View(react) : state를 보여주고, 사용자 입력으로 action을 발생

# 구조 흐름도
User input -> dispatch(action) -> reducer(state 변경) -> store(state 저장) -> view(rerender)

