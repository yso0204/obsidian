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
for idx, ch in enumerate("hello"):
    print(idx, ch)
0 h
1 e
2 l
3 l
4 o
```

## 인덱스 1부터 시작
```python
fruits = ['apple', 'banana', 'cherry']
for idx, fruit in enumerate(fruits, start=1):
    print(f"{idx}. {fruit}")
1. apple
2. banana
3. cherry
```

## 특정 조건을 만족하는 인덱스만 추출
```python
nums = [4, 8, 15, 16, 23, 42]

for i, num in enumerate(nums):
    if num % 2 == 0:
        print(f"{i}번째 요소 {num}은 짝수입니다.")

0번째 요소 4은 짝수입니다.
1번째 요소 8은 짝수입니다.
3번째 요소 16은 짝수입니다.
5번째 요소 42은 짝수입니다.
```


# enumrate() 의 내부 구조
내부적으로 아래와 같은 `generate` 객체를 생성한다.
반복 가능한데, 값은 **하나씩 천천히(lazy evalutaion)** 제공하는 구조
```python
def my_enumerate(iterable, start = 0) :
    n = start
    for elem in iterable:
        yield n,elem # 여기서 값 하나 보내주고, 다음 호출이 올 때까지 "멈춤"
        n += 1
```

실제 동작을 보면
```python
nums = [4, 8, 15, 16, 23, 42]

def my_enumerate(iterable, start = 0) :
    n = start
    for elem in iterable:
        yield n,elem
        n += 1
        
for i, num in my_enumerate(nums):
    if num % 2 == 0:
        print(f"{i}번째 요소 {num}은 짝수입니다.")

0번째 요소 4은 짝수입니다.
1번째 요소 8은 짝수입니다.
3번째 요소 16은 짝수입니다.
5번째 요소 42은 짝수입니다.
```

for문이 돌아갈 때 마다 `my_enumerate(nums)` 가 내부적으로 `yield`를 호출해서 다음 값을 생성
1. `i,num = next(my_enumerate)` - `yield 0,4`
2. `i,num = next(my_enumerate)` - `yield 1,8`