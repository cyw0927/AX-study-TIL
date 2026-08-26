# 11. 모듈과 import — 다른 코드 가져다 쓰기

Python에는 이미 만들어진 기능을 가져다 쓸 수 있다. 그때 자주 보는 말이 `import`다.

## 1. `import`는 뭐냐?

쉽게 말하면 다른 곳에 있는 기능을 현재 코드에서 쓸 수 있게 가져오는 것이다.

```python
import math
```

이제 `math` 안에 있는 여러 수학 기능을 쓸 수 있다.

## 2. 예: 제곱근 구하기

```python
import math

print(math.sqrt(16))
```

결과는 `4.0`이다.

## 3. 왜 `math.sqrt()`라고 쓰나?

`math`라는 모듈 안에 `sqrt`라는 함수가 있기 때문이다.

쉽게 말하면:

```text
math = 수학 도구상자
sqrt = 그 도구상자 안에 들어 있는 제곱근 기능
```

## 4. 필요한 것만 가져오기

```python
from math import sqrt

print(sqrt(16))
```

이제 `math.` 없이 바로 `sqrt()`를 쓸 수 있다.

## 5. 이름을 줄여 쓰기

```python
import pandas as pd
```

이 코드는 pandas를 `pd`라는 짧은 이름으로 쓰겠다는 뜻이다.

그래서:

```python
pd.DataFrame(...)
```

처럼 쓴다.

## 6. 모듈과 패키지

처음에는 둘을 엄격하게 구분하지 않아도 된다.

대충 이렇게 이해해도 된다.

- 모듈: Python 코드 파일 하나
- 패키지: 여러 모듈이 모여 있는 묶음

## 7. 기본 제공 모듈

Python을 설치하면 같이 들어오는 기능들이 있다.

예:

```python
import math
import random
import os
```

이런 것은 별도로 설치하지 않아도 되는 경우가 많다.

## 8. 외부 패키지

`pandas`, `numpy` 같은 것은 보통 따로 설치한다.

터미널에서:

```text
pip install pandas
```

처럼 설치한다.

그다음 Python 코드에서:

```python
import pandas as pd
```

로 불러온다.

## 9. `ModuleNotFoundError`

```python
import something
```

했는데 설치되어 있지 않으면 이런 오류가 날 수 있다.

```text
ModuleNotFoundError
```

이때는 보통:

1. 이름을 잘못 썼는지
2. 설치가 되어 있는지
3. 현재 Python 환경에 설치했는지

를 확인한다.

## 10. 가상환경과 import가 연결되는 이유

패키지를 설치했는데도 import가 안 될 때가 있다.

왜냐하면 터미널에서 쓰는 Python과 VS Code 또는 Jupyter가 쓰는 Python이 서로 다를 수 있기 때문이다.

그래서 패키지 문제에서는 **지금 어느 Python 환경을 쓰고 있는지**도 중요하다.

## 처음에는 이것만 기억

- `import` = 다른 기능 가져오기
- `import math` → `math.sqrt()`처럼 사용
- `from math import sqrt` → `sqrt()`처럼 바로 사용
- `as`는 별명을 붙일 때 사용
- `ModuleNotFoundError`가 뜨면 설치와 Python 환경을 확인
