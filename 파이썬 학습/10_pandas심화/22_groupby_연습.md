# pandas groupby 연습

`groupby()`는 데이터를 **같은 종류끼리 묶어서 계산**할 때 사용한다.

예를 들어 카테고리별 매출, 지역별 고객 수, 성별 평균 점수처럼 묶어서 보고 싶을 때 쓴다.

## 예제 데이터

```python
import pandas as pd

df = pd.DataFrame({
    "category": ["음료", "음료", "과자", "과자", "과자"],
    "sales": [1000, 2000, 1500, 1200, 800]
})
```

## 카테고리별 합계

```python
result = df.groupby("category")["sales"].sum()
print(result)
```

생각하는 순서:

```text
category 기준으로 묶는다
→ 각 묶음에서 sales 열을 본다
→ sum()으로 더한다
```

## 평균

```python
print(df.groupby("category")["sales"].mean())
```

## 개수

```python
print(df.groupby("category")["sales"].count())
```

## `reset_index()`

`groupby()` 결과를 다시 일반적인 표 모양으로 만들고 싶을 때 자주 쓴다.

```python
result = df.groupby("category")["sales"].sum().reset_index()
print(result)
```

## 여러 열 기준으로 묶기

```python
df = pd.DataFrame({
    "region": ["서울", "서울", "부산", "부산"],
    "gender": ["남", "여", "남", "여"],
    "sales": [100, 200, 300, 400]
})

result = df.groupby(["region", "gender"])["sales"].sum()
print(result)
```

## `agg()`

합계와 평균을 한꺼번에 보고 싶을 때 사용할 수 있다.

```python
result = df.groupby("region")["sales"].agg(["sum", "mean", "count"])
print(result)
```

## 초보자가 자주 헷갈리는 점

### `groupby()`만 써놓고 결과를 기대함

```python
df.groupby("category")
```

이것만으로는 보통 원하는 숫자 결과가 나오지 않는다. 뒤에 `sum()`, `mean()`, `count()` 같은 계산이 필요하다.

### 무엇을 기준으로 묶고 무엇을 계산하는지 헷갈림

아래처럼 문장으로 먼저 적어 보면 쉽다.

```text
카테고리별 매출 합계
```

그러면:

```text
묶는 기준 = category
계산할 열 = sales
계산 방법 = sum
```

코드는:

```python
df.groupby("category")["sales"].sum()
```

## 직접 연습

```python
import pandas as pd

df = pd.DataFrame({
    "team": ["A", "A", "B", "B", "B"],
    "score": [80, 90, 70, 60, 100]
})

print(df.groupby("team")["score"].sum())
print(df.groupby("team")["score"].mean())
print(df.groupby("team")["score"].count())
```

각 결과를 손으로 먼저 계산한 다음 실행 결과와 비교한다.
