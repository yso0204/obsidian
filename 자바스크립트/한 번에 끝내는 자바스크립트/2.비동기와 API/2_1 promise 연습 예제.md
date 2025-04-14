# 📘 자바스크립트 Promise 예제 모음

  

## ✅ 예제 1: 가장 기본적인 Promise

```js

const myPromise = new Promise((resolve, reject) => {

  setTimeout(() => {

    resolve('👍 성공했어요!');

  }, 1000);

});

  

myPromise.then((result) => {

  console.log('결과:', result);

});

```

  

---

  

## ✅ 예제 2: 실패하는 Promise (`reject`)

```js

const failPromise = new Promise((resolve, reject) => {

  setTimeout(() => {

    reject('❌ 실패했어요!');

  }, 1000);

});

  

failPromise

  .then((result) => {

    console.log('성공:', result);

  })

  .catch((err) => {

    console.error('실패:', err);

  });

```

  

---

  

## ✅ 예제 3: Promise 체이닝 (return 꼭 하기)

```js

const addFive = (v) => {

  return new Promise((resolve) => {

    setTimeout(() => {

      console.log(`addFive: ${v} + 5`);

      resolve(v + 5);

    }, 1000);

  });

};

  

const double = (v) => {

  return new Promise((resolve) => {

    setTimeout(() => {

      console.log(`double: ${v} * 2`);

      resolve(v * 2);

    }, 1000);

  });

};

  

addFive(10)

  .then((res1) => {

    return double(res1);

  })

  .then((res2) => {

    console.log('최종 결과:', res2);

  });

```

  

---

  

## ❌ 예제 4: return 빠진 경우 (실패 예시)

```js

addFive(10)

  .then((res1) => {

    double(res1); // ❌ return 빠짐

  })

  .then((res2) => {

    console.log('res2:', res2); // ❌ undefined

  });

```

  

---

  

## ✅ 예제 5: async/await로 동일한 코드

```js

async function run() {

  const res1 = await addFive(10);

  const res2 = await double(res1);

  console.log('최종 결과:', res2);

}

  

run();

```

  

---

  

## ✅ 예제 6: 여러 작업 동시에 실행 (Promise.all)

```js

const delay = (msg, time) => {

  return new Promise((resolve) => {

    setTimeout(() => {

      resolve(msg);

    }, time);

  });

};

  

Promise.all([

  delay('🍜 라면 끓이기', 3000),

  delay('🥚 계란 삶기', 2000),

  delay('🍚 밥 짓기', 4000)

]).then((results) => {

  console.log('모든 요리 완료!');

  console.log(results); // ['🍜 라면 끓이기', '🥚 계란 삶기', '🍚 밥 짓기']

});

```

  

---

  

## ✅ 예제 7: 일부 실패하면 (Promise.all 에러 처리)

```js

const success = () => Promise.resolve('성공!');

const fail = () => Promise.reject('에러!');

  

Promise.all([success(), fail(), success()])

  .then((res) => {

    console.log('All OK:', res);

  })

  .catch((err) => {

    console.error('⚠️ 하나라도 실패:', err);

  });

```