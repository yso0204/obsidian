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

