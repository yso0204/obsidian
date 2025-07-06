> 파이썬 내장 함수로, 리스트나 튜플 같은 반복 가능한 (iterable) 객체를 순회할 때, index와 값을 동시에 얻을 수 있게 해주는 유용한 함수

# 동작원리
`enumrate()`는 iterable 한 객체(리스트, 튜플, 문자열) 를 받아, 각 요소에 index를 붙여서 tuple 형태로 반환하는 객체를 만들어 줌
```python
fruits = ['apple','banana','cherry']
result = enumrate(fruits)

print(result)  # <enumerate object at 0x...> ← 이건 이터레이터 객체
print(list(result))  # [(0, 'apple'), (1, 'banana'), (2, 'cherry')]
```
즉, `enumrate()` 자체는 메모리를 아끼기 위해 **지연 평가(lazy evaluation)** 를 사용하는 이터레이터를 반환하고, `list()`로 감싸면 그 내용을 한꺼번에 펼쳐서 볼 수 있다.

# 왜 `enumrate()`를 쓰는가?
## 기존 방식의 문제점
```python
for i in range(len(fruits)):
	print(i, fruits[i])
```
- `len(fruits)`는 매번 호출됨(비효율적)
- 인덱스와 값을 따로 관리해야 하므로 가독성이 낮다

## enumrate 방식
```python
for i, fruit in enumrate(fruits):
	print(i,fruit)
```
- 인덱스와 값을 한 번에 받아서 코드가 깔끔하고 직관적
- 이터레이터 기반이라 메모리 효율성도 높음

# 활용 예제
## 문자열 순회
```python
```
