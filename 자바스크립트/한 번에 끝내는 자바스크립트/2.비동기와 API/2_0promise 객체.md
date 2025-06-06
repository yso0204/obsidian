## 콜백 지옥
```js
function increaseAndPrint(n, callback) {
    setTimeout(() => {
        const increased = n + 1;
        console.log(increased);
        if (callback) {
            callback(increased);
        }
    }, 1000);
}

increaseAndPrint(0, n => {
    increaseAndPrint(n, n => {
        increaseAndPrint(n, n => {
            increaseAndPrint(n, n => {
                console.log('done');
            })
        })
    })
})

1
2
3
4
```
> callback이 중첩되면서 depth가 깊어져 가독성이 망가진다

## promise로 변경하면?

```js
function increaseAndPrint(n) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log(n + 1);
            resolve(n + 1);
        }, 1000);
    })
}

increaseAndPrint(0)
    .then((rst) => {
        return increaseAndPrint(rst)
    })
    .then((rst) => {
        return increaseAndPrint(rst)
    })
    .then((rst) => {
        return increaseAndPrint(rst)
    });

```

## Promise 생성
> `new` 키워드와 생성자를 사용해 생성
> `executor`라는 실행 함수를 전달하고, `resolve`와 `reject`라는 콜백 함수를 전달

## `executor` 란
실행 함수로 promise 생성자에 반드시 전달해야 하는 함수로 promise 객체가 생성될 때 자동으로 실행되는 함수.

원하는 어떠한 작업이 실행되며 성공하면 `resolve` 실패하면 `reject`를 호출한다. 

![](https://i.imgur.com/22lbroE.png)

# Promise 객체 처리
>promise는 세 가지 상태를 가질 수 있다.
1. 대기(pending) : 아직 작업이 끝나지 않은 상태
2. 이행(fulfilled) : 작업이 성공으로 끝난 상태 -> `.then()`으로 결과 받음
3. 거부(reject) : 작업이 실패한 상태 -> `.catch()`로 에러 처리

```js
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('실패')
        resolve('성공')
    }, 1000);
})

promise.then((result) => {
    console.log('성공',result);
}).catch((error) => {
    console.log(error);
})
```

## Promise 함수 등록
```js
//promise 객체를 반환하는 함수
function myPromise(temp) {
    return new Promise((resolve, reject) => {
        if (/*promise의 성공 조건*/temp%2==0) {
            resolve();
        }
        else {
            reject();
        }
    })
}

//promise 객체를 반환하는 함수 call
myPromise(9)
    .then((result) => {
        //성공시 resolve('')의 '' 값 result로 리턴됨
    })
    .catch((error) => {
        //성공시 error('')의 '' 값 error로 리턴됨
    })

```

1. 재사용성 : promise 객체를 필요할 때 마다 호출하여 재사용 가능
2. 가독성 : promise 객체를 함수로 만들어 두면 비동기 작업의 정의와 사용이 분리되어 가독성이 좋아진다.
3. 확장성 : 함수에 파라미터를 넘겨 동적으로 비동기 작업을 수행할 수 있고 여러 개의 promise 객체를 반환하는 함수를 연결할 수 있다.
3.확장성 관련 보충
- 동적으로 비동기 작업?
```js
function fetchUser(id) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(`유저 ${id} 정보 가져옴`);
    }, 1000);
  });
}

fetchUser(1).then(console.log); // 유저 1 정보 가져옴
fetchUser(2).then(console.log); // 유저 2 정보 가져옴
```

id를 바꾸면 다른 사용자에 대해 비동기 작업을 수행할 수 있는데 이게 **동적**이다.

- 여러 개의 promise 함수를 연결?
```js
function step1(v) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log('1step done');
            resolve(v + 1);
        }, 500);
    });
}
function step2(v) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log('2step done');
            resolve(v * 2);
        }, 500);
    });
}
function step3(v) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log('3step done');
            resolve(v - 3);
        }, 500);
    });
}

step1(5)
    .then((rst) => {
        return step2(rst)
    })
    .then((rst) => {
        return step3(rst)
    })
    .then((rst) => {
        console.log('alldone',rst)
    })
```

체이닝이 가능하다 라는 의미

참고로 위에 `then`과 아래는 같음
```js
step1(5)
  .then(step2)
  .then(step3)
  .then((result) => {
    console.log('최종 결과:', result); // ((5+1)*2)-3 = 9
  });
```

`.then(step2)`는 위에 풀어쓴거랑 동일하게 동작하는데
즉, 함수 이름만 넘겨도 자동으로 호출하는 함수로 바뀐다.
단, 넘기는 함수는 반드시 `promise`를 반환해야 체이닝이 유지됨

## promise chaining
> then 메서드를 연속으로 사용하는 방식

```js
const workA = (value) => {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve(value + 5);
        }, 5000);
    })
};
const workB = (value) => {
    return new Promise((resovle) => {
        setTimeout(() => {
            resovle(value - 3);
        }, 3000);
    })
};
const workC = (value) => {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve(value + 10);
        }, 10000);
    })
};

workA(10)
  .then((resA) => {
    console.log(`workA : ${resA}`);
    return workB(resA);//Promise를 return 해야 다음 then으로 연결됨
  })
  .then((resB) => {
    console.log(`workB : ${resB}`);
    return workC(resB);
  })
  .then((resC) => {
    console.log(`workC : ${resC}`);
  })
  .catch((err) => {
    console.error('에러 발생:', err);
  });

```

## then,catch,finally는 promise를 반환
> 결국 체이닝과 관련되어 있는데
> `then()` `catch()` `finally()`는 원래 promise를 수정하지 않고 항상 새로운 promise 객체를 반환한다.

`(...)`은 항상 함수를 넣어야 하며 만약 다른 promise 객체 같은걸 넣으면 무시된다.

이는 체이닝이 가능한 이유로 연결되는데,
```js
doSomething()
  .then((res) => step1(res))
  .then((res) => step2(res))
  .then((res) => step3(res))
  .catch((err) => handleError(err));
```
각 `then()`이 새로운 promise를 반환하기에 이어지는 것

```js
const p = Promise.reject('에러!');

const p2 = p.catch((err) => {
  console.log('에러 처리:', err);
  return '정상복구';
});

p2.then((res) => {
  console.log('결과:', res); // 정상복구
});

에러 처리: 에러!
결과: 정상복구
```
`catch()`도 promise를 반환하기에 `.then()`으로 이어서 가능


# Promise 정적 메서드
> promise 클래스에는 5가지의 정적 메서드가 있다

## Promise.resolve()
> 즉시 성공(resolve) 상태의 promise를 생성
> 비동기가 필요 없지만, promise로 다루고 싶을 때 사용한다

```js
const p = Promise.resolve(42);

p.then((v) => {
  console.log('값:', v); // 값: 42
});
```
- 활용 : 테스트, 초기값 감싸기, 체이닝 시작점으로 사용

## Promise.reject
> 즉시 실패(reject) 상태의 promise를 생성
> 일부러 에러를 발생시키거나 테스트용으로 사용한다.

```js
const p = Promise.reject('에러 발생!');

p.catch((err) => {
  console.log('에러 처리:', err); // 에러 처리: 에러 발생!
});
```
- 활용 : 실패 흐름 테스트, 조건 분기
## Promise.all(iterable)
> 여러 개의 Promise를 병렬로 실행하고, **전부 성공하면** 결과 배열을 반환
> 하나라도 실패하면 `.catch()`로 감

```js
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);
//const p3 = Promise.reject(3);
Promise.all([p1, p2, p3])
  .then((results) => {
    console.log('결과:', results); // [1, 2, 3]
  })
  .catch((err) => {
    console.error('에러:', err);// 에러 : 3
  });
```

- 활용 : 병렬 요청, 전부 완료가 필요할 때(이미지 여러 개 불러 오기 등)

## Promise.allsettled(iterable)
> all 과는 조금 다르게 모든 Promise들의 성공.실패 결과를 반환한다.
> 실패하더라도 `.catch`로 넘어가지 않음

```js
const p1 = new Promise(reseolve => setTimeout(() => {
    reseolve(1)
}, 1000));
const p2 = new Promise((reseolve,reject) => setTimeout(() => {
    reject(new Error('error 발생'))
}, 2000));
const p3 = new Promise(reseolve => setTimeout(() => {
    reseolve(3)
}, 4000));

Promise.allSettled([p1, p2, p3])
    .then((result) => {
        console.log(result);
    })

[
  { status: 'fulfilled', value: 1 },
  {
    status: 'rejected',
    reason: Error: error 발생
        at Timeout._onTimeout (C:\Users\sahak\OneDrive\바탕 화면\study\js\한번에끝내는자바스크립트\src\index.js:5:12)       
        at listOnTimeout (node:internal/timers:573:17)
        at process.processTimers (node:internal/timers:514:7)
  },
  { status: 'fulfilled', value: 3 }
]
```

- 활용 : 성공,실패 상관없이 전체 결과 확인이 필요할 때

## Promise.race(iterable)
> 가장 먼저 완료된 Promise 결과를 반환
> 성공이던 실패든 먼저 끝난 놈이 이김

```js
const fast = new Promise((resolve) => setTimeout(() => resolve('빠름'), 100));
const slow = new Promise((resolve) => setTimeout(() => resolve('느림'), 1000));

Promise.race([fast, slow]).then((res) => {
  console.log(res); // 빠름
});

const failFast = new Promise((_, reject) => setTimeout(() => reject('실패'), 100));
const slowOK = new Promise((resolve) => setTimeout(() => resolve('정상'), 1000));

Promise.race([failFast, slowOK])
  .then((res) => console.log(res))
  .catch((err) => console.error('에러:', err)); // 에러: 실패

```
- 활용 : 타임 아웃 처리, 응답 중 가장 빠른 것을 사용

## Promise.any(iterable) - ES2021
> 하나라도 성공하면 성공, 전부 실패해야 `.catch`로 감
> 성공한 값들 중 가장 먼저 도착한 것을 반환한다

```js
const p1 = Promise.reject('실패1');
const p2 = Promise.resolve('성공!');
const p3 = Promise.reject('실패2');

Promise.any([p1, p2, p3])
  .then((res) => {
    console.log('성공:', res); // 성공: 성공!
  })
  .catch((err) => {
    console.error('전부 실패:', err);
  });
```