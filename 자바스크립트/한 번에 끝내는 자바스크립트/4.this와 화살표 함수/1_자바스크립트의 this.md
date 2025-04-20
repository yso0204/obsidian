# this 란?
> 자신이 속한 객체를 가리키는 키워드로 Javascript 함수와 관려이 있다.
> js에서 this 키워드는 함수가 어떻게 호출되었는가? 에 따라 바인딩 되는 값이 동적으로 결정된다.

- 일반적인 다른 언어에서 쓰이는 this 와는 약간 다르다
# C++ 에서의 this
```c++
class Person {
private:
    string name;

public:
    Person(string name) {
        this->name = name; // 왼쪽은 멤버 변수, 오른쪽은 매개변수
    }

    void introduce() {
        cout << "Hi, I'm " << this->name << endl;
    }
};
```

- `this`는 항상 현재 인스턴스의 주소를 가리키는 포인터로 this->멤버 같은 형태로 사용한다.
## js 함수 호출 방식
1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. 콜백 함수 호출

## 전역 공간에서의 this
```js
console.log(this);
```
![](https://i.imgur.com/sBNovrY.png)
- node에서 실행하면 `global`이 출력됨

## 일반 함수 호출
```js
function show() {
    console.log(this);
}
show();
```
![](https://i.imgur.com/sBNovrY.png)
- `this`는 자신을 포함하고 있는 함수가 어떻게 호출되었는가? 에 따라서 값이 달라는데, 여기서는 `this`가 포함된 `func` 함수를 호출한 객체가 `window`이기에 `window`가 바인딩 된다.
## 메서드 호출
```js
const person = {
    name: 'tom',
    sayHi() {
        console.log(this.name);
    }
}

person.sayHi();
```
![](https://i.imgur.com/LI455yO.png)

메서드 : 객체 프로퍼티의 함수

함수를 메서드로써 호출하면, 그 메서드를 포함하고 있는 그 객체가 호출됨

### 객체 속에 객체의 프로퍼티
```js
const cafe = {
    brand: '이디야',
    menu: '아메리카노',
    newCafe: {
        brand: '이디야',
        menu: '라떼',
        print: function () {
            console.log(this);
        },
    },
};

cafe.newCafe.print();
```
![](https://i.imgur.com/XOcxRxs.png)

newCafe라는 객체가 출력됨
즉 `print()`를 호출하는 주체(호출 컨텍스트)는 `cafe.newCafe`

### 아래처럼 바뀌면?
```js
const cafe2 = {
    brand: '할리스',
    menu: '아메리카노',
    print: function () {
        console.log(this);
    },
};

const myCafe = cafe2.print;
myCafe();
```
![](https://i.imgur.com/LIUTz3O.png)
`myCafe`에 `cafe2.print`함수만 복사된 형태이다.
그렇기에 myCafe()는 일반 함수로 호출되어 `window`가 출력된다.

## 생성자 함수 호출
```js
function cafe(menu) {
    console.log(this);
    this.menu = menu;
}

let myCafe = new cafe('latte');
console.log(myCafe);
let myCafe2 = cafe('latte');
console.log(myCafe2);
```
![](https://i.imgur.com/DKVhAi7.png)
`myCafe`는 `new`를 사용하여 새로운 객체로 만들어 주었기에 myCafe 의`consol.log(this)`는 `this.menu`가 할당 전이기에 빈 객체를 보여주고 있고
이후 `myCafe`에 latte 가 할당되어 myCafe 객체의 menu에 해당 값이 있다.

자바스크립트 내부적으로는 아래와 같이 동작한다.
```js
let thisObj = {};              // 새 객체 생성
thisObj.__proto__ = cafe.prototype; // 프로토타입 연결
cafe.call(thisObj, 'latte');   // thisObj를 this로 바인딩하고 함수 호출
return thisObj;
```

`console.log(this)` 는 `thisObj`를 출력
- 함수 안에서 `this`는 `thisObj`이므로 `this.menu = menu`는 `thisObj.menu = 'latte'`로 저장
그렇기에 `cafe { menu: 'latte' }` 로 출력된다.

그러나 `myCafe2`는 `cafe`함수 자체를 가리키고 있고, `cafe`함수는 return 값이 없다.

그렇기에 `cafe` 함수에서 this는 어떤 객체를 가리키고 있는지를 출력해야하는데 일반 함수로써 호출되었기에 `window`를 출력하고, `myCafe2`를 출력해보면 `cafe` 함수는 return 이 없기에 `undefined`가 return 되어 `undefined`가 출력된다.


## 콜백 함수
```js
const cafe = {
    brand: '이디야',
    menu: '',
    setMenu: function (menu) {
        this.menu = menu;
    },
};

function getMenu(menu, callback) {
    callback(menu);
}

getMenu('핫초코', cafe.setMenu);

console.log(cafe);
console.log(window.menu);
```

![](https://i.imgur.com/IfoCK2o.png)

js에서의 `this`는 자신을 포함하고 있는 함수가 어떻게 호출되었는가? 에 따라서 값이 달라진다.

`setMenu`는 `getMenu`에서 메서드가 아닌, 일반 함수로써 호출되었다.
그렇기에 `this`는 전역객체인 window를 가리키고 있고, 그래서 `winodw.menu`가 핫초코 라는 값을 가지고 있다.

만약에 아래처럼 바꾸면 다를 것이다.
```js
function getMenu(menu) {
    cafe.setMenu(menu);
}
```
![](https://i.imgur.com/DcOpnND.png)
