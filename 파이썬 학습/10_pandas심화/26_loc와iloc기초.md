# pandas loc와 iloc 기초

pandas DataFrame에서 원하는 행이나 열을 골라 볼 때 `loc`와 `iloc`를 자주 만난다.

처음에는 이렇게 기억하면 된다.

```text
loc  → 이름으로 찾는 느낌
iloc → 번호로 찾는 느낌
```

예제:

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["철수", "영희", "민수"],
    "score": [80, 90, 70]
})
```

## iloc

```python
print(df.iloc[0])
```

첫 번째 행을 가져온다.

Python은 0부터 세므로 `0`은 첫 번째다.

```python
print(df.iloc[1])
```

두 번째 행이다.

행과 열을 번호로 함께 고를 수도 있다.

```python
print(df.iloc[0, 1])
```

첫 번째 행의 두 번째 열 값을 가져온다.

## loc

`loc`는 행 이름과 열 이름을 사용한다.

```python
print(df.loc[0, "name"])
```

결과는 `철수`다.

조건식과 함께 자주 쓴다.

```python
print(df.loc[df["score"] >= 80])
```

점수가 80 이상인 행만 가져온다.

## 열 여러 개 선택

```python
print(df.loc[:, ["name", "score"]])
```

여기서 첫 번째 `:`는 모든 행이라는 뜻이다.

## 헷갈릴 때

```text
iloc[0]       → 첫 번째 행
loc[0]        → 인덱스 이름이 0인 행
iloc[0, 1]    → 첫 번째 행, 두 번째 열
loc[0, "name"] → 인덱스 0, name 열
```

처음부터 외우지 말고 작은 DataFrame을 만든 뒤 직접 하나씩 출력해 보는 게 가장 빠르다.
