
## 생성
> `new` 키워드와 생성자를 사용해 생성
> `executor`라는 실행 함수를 전달하고, `resolve`와 `reject`라는 콜백 함수를 전달

## `executor` 란
실행 함수로 promise 생성자에 반드시 전달해야 하는 함수로 promise 객체가 생성될 때 자동으로 실행되는 함수.

원하는 어떠한 작업이 실행되며 성공하면 `resolve` 실패하면 `reject`를 호출한다. 

![](https://i.imgur.com/22lbroE.png)

promise는 세 가지 상태를 가질 수 있다.
1. 대기(pending) : 아직 작업이 끝나지 않은 상태
2. 이행(fulfilled) : 작업이 성공으로 끝난 상태 -> `.then()`으로 결과 받음
3. 거부(reject) : 작업이 실패한 상태 -> `.catch()`로 에러 처리
