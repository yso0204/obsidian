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
메모리에 모든 값을 저장하는 `list`와 달리 필요할 때 마다 하나
