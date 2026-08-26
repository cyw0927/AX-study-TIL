# 18. NumPy 첫걸음

NumPy는 숫자를 많이 다룰 때 자주 쓰는 Python 라이브러리다. 처음에는 **숫자 리스트를 더 편하게 계산하게 해주는 도구**라고 생각하면 된다.

## 왜 그냥 리스트를 안 쓰지?

Python 리스트도 숫자를 저장할 수 있다.

```python
numbers = [1, 2, 3, 4]
```

하지만 리스트에 10을 더한다고 해서 모든 숫자에 10이 더해지지는 않는다.

```python
print(numbers + [10])
```

결과는 숫자 계산이 아니라 리스트 뒤에 10이 붙는다.

NumPy 배열은 다르게 동작한다.

```python
import numpy as np

numbers = np.array([1, 2, 3, 4])
print(numbers + 10)
```

결과:

```text
[11 12 13 14]
```

## 설치

터미널에서:

```text
pip install numpy
```

주의: 이건 Python 코드가 아니라 터미널 명령어다.

## `import numpy as np`

```python
import numpy as np
```

NumPy를 가져오고 앞으로 `np`라는 짧은 이름으로 부르겠다는 뜻이다.

## `np.array()`

리스트를 NumPy 배열로 바꿀 수 있다.

```python
import numpy as np

a = np.array([10, 20, 30])
print(a)
print(type(a))
```

## 배열 계산

```python
import numpy as np

a = np.array([1, 2, 3])

print(a + 10)
print(a * 2)
print(a / 2)
```

각 원소에 계산이 한꺼번에 적용된다.

## 평균과 합계

```python
import numpy as np

scores = np.array([80, 90, 70, 100])

print(scores.sum())
print(scores.mean())
print(scores.max())
print(scores.min())
```

## 2차원 배열

표처럼 행과 열을 가진 배열도 만들 수 있다.

```python
import numpy as np

arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr)
print(arr.shape)
```

`shape`는 배열의 모양이다.

```text
(2, 3)
```

이면 2행 3열이라는 뜻이다.

## 인덱스

```python
print(arr[0, 0])
print(arr[1, 2])
```

첫 번째는 1, 두 번째는 6이다.

## 초보가 기억할 것

```text
np.array() = NumPy 배열 만들기
.shape     = 행과 열 크기 보기
.sum()     = 합계
.mean()    = 평균
.max()     = 최댓값
.min()     = 최솟값
```

NumPy는 pandas나 이미지 처리에서도 자주 만나게 된다. 처음에는 복잡한 행렬 계산보다 리스트와 무엇이 다른지를 이해하는 것이 먼저다.
