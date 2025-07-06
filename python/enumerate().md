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
	- 메모리 효율성이 높다는 뜻은?
		- 단순 리스트로 불러오면 리스트 내 모든 값을 메모리에 올리고 시작
		- `enumrate()`는 그 순간에 딱 하나만 꺼내서 사용하므로 메모리면에서 이득

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
3. ....
`yield`는 매번 값을 하나씩 반환하고, 멈춰 있다가 다음 루프에서 다시 이어서 실행된다.

## 일반 함수 vs 제너레이터 함수
|함수 종류|반환 키워드|반환 시 동작|상태 기억|
|---|---|---|---|
|일반 함수|`return`|바로 종료|❌|
|제너레이터|`yield`|값 주고 일시정지|✅ 함수 내부 상태 기억함|

# dictionary에서의 enumerate
## dictionary에 enumerate 반복?
단순히 dictionary에 enumerate를 사용하면 의도와는 다소 다를 수 있다.
```python
dic = {
    'a':'A',
    'b':'B',
    'c':'C'
}

print(dic.items())

for key,value in dic.items():
    print(f'dic[{key}]={value}')

dic[a]=A
dic[b]=B
dic[c]=C

for key,value in enumerate(dic):
    print(f'dic[{key}] : {value}')

dic[0] : a
dic[1] : b
dic[2] : c
```

우리는 `key`와 `value`가 나오지 않을까? 라고 예상했지만 `dictionary`는 반복하면 기본적으로 `key`만 꺼내기 때문에 `enumerate`는 `key`값에 번호만 붙인 형태가 된다.


## `items()` 사용
```python
for i, (key, value) in enumerate(dic.items()):
    print(i, key, value)

0 a A
1 b B
2 c C
```

여기서 `items()`는 dictionary의 `(key,value)`쌍을 꺼내준다.
`enumerate`는 여기에 번호만 붙이는 것

