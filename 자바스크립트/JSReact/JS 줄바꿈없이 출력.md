> console.log는 기본적으로 호출될 때마다 줄바꿈(`\n`)이 자동으로 들어가서 다음 출력이 새로운 줄에 나온다

이를 줄바꿈 없이 한 줄에 계속 출력하고 싶다면?

## Node.js
```js
process.stdout.write('hello')
```

- 단 이 방법은 문제가 있는데, 파라미터로 오는 값이 항상 string 타입이어여 한다.
- `process.stdout.write(chunk[, encoding][, callback])`
	- chunk : 출력할 데이터 : 문자열 또는 버퍼
	- encoding : 문자열 인코딩(UTF-8이 보통 default)
	- callbak : 출력 완료 후 실행할 콜백
## 브라우저 환경(DOM에 출력)
> 문자열을 한번에 출력해야 됨

```js
let msg = "";
msg += "hello ";
msg += "world";
console.log(msg);
```