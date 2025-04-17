![](https://i.imgur.com/TGc6BPt.png)
> form 태그는 웹 페이지에서 사용자로부터 데이터를 수집하거나 상호작용을 위해 사용된다.

## select / label

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Form Test</title>
        <meta charset="UTF-8" />
    </head>
    <body>
        <label for="fruitSelect">과일 선택:</label>
        <select id="fruitSelect">
            <option value="apple">사과</option>
            <option value="banana" selected>바나나</option>
            <option value="cherry">체리</option>
            <option value="grape">포도</option>
        </select>
        <script src="src/index.js"></script>
    </body>
</html>
```
`label`에 for 속성값에 특정 form의 id 를 할당하면 클릭할 때 자동으로 해당 입력 요소에 포커스가 가거나, 활성화된다.
![](https://i.imgur.com/ci0RlFh.png)


`select` 태그에는 여러가지의 옵션 중 하나를 선택할 수 있게 드롭다운 목록을 `option` 태그를 사용하여 작성한다.

또한 `option` 태그에 selected 속성을 작성하여 기본값을 설정할 수 있다.

`index.js`
```js
const $fruitSelect = document.getElementById('fruitSelect');

$fruitSelect.addEventListener('change', (event) => {
    let selectedValue = event.target.value;
    console.log(selectedValue);
});
```
이렇게 event 만들어서 실행도 가능하다.

## input
> 특정 값을 입력하기 위해 사용되는 태그

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Form Test</title>
        <meta charset="UTF-8" />
    </head>
    <body>
        <label for="userName">이름 : </label>
        <input type="text" id="userName" placeholder="이름을 입력"/>
        <label for="password">비밀번호:</label>
        <input type="password" id="password" placeholder="비밀번호를 입력하세요" />

        <button>로그인</button>

        <script src="src/index.js"></script>
    </body>
</html>
```
`input` 태그에서 `type`에는 다양한 값들이 있는데 `password` 같이 type에 맞게 설정하면 비밀번호가 숨김처리 되며, 숫자만 입력할 수 있게 하는 등의 기능이 있다.

`label`은 단순히 '이름' 같은 텍스트만 보여주는 것이 아닌 해당 입력 요소(input의 id)와 연결되는 이름표 역할을 한다.
1. 이름 / 비밀번호 텍스트를 클릭하면 input 창으로 포커스가 간다
2. 화면 낭독기 등을 사용할 때 label 덕분에 input의 의미를 정확히 파악할 수 있다.
```html
<p>이름:<input type="text" id="userName" placeholder="이름을 입력"/></p>
```
이거랑은 생긴건 비슷할 수 있어도 기능적으로 완전히 다름

마찬가지로 버튼에 이벤트를 줄 수 있다.
```js
const $userName = document.getElementById('userName');
const $password = document.getElementById('password');

const $loginBtn = document.querySelector('button');

$loginBtn.addEventListener('click', () => {
    console.log($userName.value);
    console.log($password.value);
});
```
혹은
```js
$userName.value = '홍길동';
$password.addEventListener('input', (event) => {
    console.log(event.target.value);
});
```
이렇게 해서도 `input` 태그의 값을 가져와서 조작할 수 있다.

