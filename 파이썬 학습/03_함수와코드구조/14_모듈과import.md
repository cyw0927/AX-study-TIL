# 14. 모듈과 import

Python 파일이 많아지면 코드를 한 파일에 전부 넣지 않고 나눠서 관리하게 된다. 이때 자주 나오는 말이 **모듈(module)** 이다.

## 모듈이란?

간단히 말하면 **Python 코드가 들어 있는 파일**이다.

예를 들어 `calculator.py`라는 파일이 있다고 하자.

```python
def add(a, b):
    return a + b


def subtract(a, b):
    return a - b
```

다른 Python 파일에서 이 기능을 가져다 쓸 수 있다.

## `import`

다른 모듈을 가져오는 문법이다.

```python
import calculator

print(calculator.add(3, 5))
```

`calculator.py` 안에 있는 `add()` 함수를 사용하는 것이다.

## 특정 함수만 가져오기

```python
from calculator import add

print(add(3, 5))
```

이 경우에는 `calculator.add()`라고 쓰지 않고 바로 `add()`라고 쓸 수 있다.

## `as`

긴 이름을 짧게 바꿔서 사용할 수 있다.

```python
import pandas as pd
```

이후에는:

```python
pd.DataFrame(...)
```

처럼 쓴다.

`pd`는 pandas가 특별히 정한 문법이 아니라 사람들이 자주 사용하는 별명이다.

## Python 기본 모듈

Python 설치만 해도 사용할 수 있는 모듈이 있다.

### `math`

```python
import math

print(math.sqrt(16))
print(math.pi)
```

### `random`

```python
import random

print(random.randint(1, 10))
```

### `os`

파일 경로나 폴더 같은 운영체제 기능을 다룰 때 사용한다.

```python
import os
print(os.getcwd())
```

## 모듈과 패키지는 뭐가 다른가?

처음에는 다음 정도로 이해하면 된다.

```text
모듈   → Python 파일 하나
패키지 → 여러 모듈을 묶은 더 큰 단위
```

실제로는 더 복잡한 개념이 있지만 초보 단계에서는 이 정도면 충분하다.

## `if __name__ == "__main__":`

Python 파일 아래쪽에서 자주 볼 수 있다.

```python
def main():
    print("프로그램 시작")


if __name__ == "__main__":
    main()
```

뜻은 대략:

> 이 파일을 직접 실행했을 때만 main()을 실행한다.

다른 파일에서 이 파일을 `import`했을 때는 `main()`이 자동으로 실행되지 않도록 한다.

처음에는 문장을 외우기보다 **직접 실행용 코드와 import용 코드를 구분하는 장치**라고 이해하면 된다.

## import 오류가 날 때

### `ModuleNotFoundError`

```text
ModuleNotFoundError: No module named 'pandas'
```

이런 오류가 나면 보통 해당 패키지가 설치되어 있지 않거나, 설치한 Python 환경과 현재 실행 환경이 다를 수 있다.

확인:

```powershell
python -m pip list
```

## 직접 연습

`my_math.py`:

```python
def double(number):
    return number * 2
```

`main.py`:

```python
from my_math import double

print(double(10))
```

두 파일을 같은 폴더에 만들고 `main.py`를 실행해 본다.
