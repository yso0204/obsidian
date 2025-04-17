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

