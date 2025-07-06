> list와 비슷해보이지만, 더 가벼운 기능

# 기본 사용법
```python
range(stop)            # 0부터 stop 직전까지
range(start, stop)     # start부터 stop 직전까지
range(start, stop, step)  # step 간격으로 증가

range(5)         → 0, 1, 2, 3, 4
range(2, 6)      → 2, 3, 4, 5
range(1, 10, 2)  → 1, 3, 5, 7, 9
range(10, 0, -1) → 10, 9, ..., 1
```

# `range()`는 리스트인가?
`range()`는 range 객체로 리스트가 아니다.
메모리에 모든 값을 저장하는 `list`와 달리 필요할 때 마다 하나씩 생성하는 `lazy evaluation` 이다.

## 메모리 비교
```python
import sys

print(sys.getsizeof(range(1000000)))
print(sys.getsizeof(list(range(1000000))))

48
8000056
```

## type?
```python
print(type(range(5)))

<class 'range'>
```
- 리스트나 튜플이 아닌 range 객체
- `__iter__()` 메서드를 갖고 있어서 반복 가능한 iterable

| 특징     | 내용                           |
| ------ | ---------------------------- |
| 기본 형식  | `range(start, stop, step)`   |
| 포함 범위  | 시작값 포함, 끝값 제외 (`stop - 1`까지) |
| 타입     | `range` 객체 (`list` 아님)       |
| 메모리    | 매우 효율적 (지연 계산 방식)            |
| 리스트 변환 | `list(range(...))`로 가능       |
| 반복 사용  | `for`, `in` 문에서 매우 유용        |
| 사용 이유  | 빠르고, 가볍고, 범위 생성에 특화됨         |

