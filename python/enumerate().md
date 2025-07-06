> 파이썬 내장 함수로, 리스트나 튜플 같은 반복 가능한 (iterable) 객체를 순회할 때, index와 값을 동시에 얻을 수 있게 해주는 유용한 함수

# 동작원리
`enumrate()`는 iterable 한 객체(리스트, 튜플, 문자열) 를 받아, 각 요소에 index를 붙여서 tuple 형태로 반환하는 객체를 만들어 줌
```python
fruits = ['apple','banana','cherry']
result = enumrate(fruits)

print(result)  # <enumerate object at 0x...> ← 이건 이터레이터 객체
print(list(result))  # [(0, 'apple'), (1, 'banana'), (2, 'cherry')]
```
즉, `enumrate` 자체