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

promise는 세 가지 상태를 가질 수 있다.
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

## 콜백 지옥
> promise를 이용해 자바스크립트 비동기 처리 방식의 문제점 중 하나인 콜백 지옥을 해결 할 수 있다.

```js
const workA = (value, callback) => {
    setTimeout(() => {
        callback(value + 5);
    }, 5000);
};
const workB = (value, callback) => {
    setTimeout(() => {
        callback(value - 3);
    }, 3000);
};
const workC = (value, callback) => {
    setTimeout(() => {
        callback(value + 10);
    }, 10000);
};

workA(10, (resA) => {
    console.log(`workA : ${resA}`);
    workB(resA, (resB) => {
        console.log(`workB : ${resB}`);
        workC(resB, (resC) => {
            console.log(`workC : ${resC}`);
        });
    });
});
```

workA -> workB -> workC로 진행되는데 중간 수정도 어렵고 어디까지 callback인지 구별도 어려움

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