# 13. pandas 필터링과 결측치

pandas를 쓰다 보면 가장 자주 하는 일이 **원하는 행만 골라내는 것**과 **비어 있는 값을 확인하는 것**이다.

처음에는 대괄호가 많아서 헷갈리지만, 순서를 쪼개서 보면 생각보다 단순하다.

## 1. 조건식은 True / False를 만든다

```python
customers["age"] >= 30
```

이 코드는 30세 이상 고객을 바로 보여주는 것이 아니라, 각 행마다 조건이 맞는지 `True`, `False`를 만든다.

그 결과를 DataFrame에 다시 넣으면 조건에 맞는 행만 남는다.

```python
customers_over_30 = customers[
    customers["age"] >= 30
]
```

이 방식을 Boolean Mask라고 한다.

## 2. 여러 조건을 같이 쓰기

pandas에서는 일반 Python 조건문의 `and`, `or`, `not` 대신 보통 다음 기호를 쓴다.

```text
&  → 그리고
|  → 또는
~  → 부정
```

예를 들어 30세 이상이면서 서울 거주 고객:

```python
result = customers[
    (customers["age"] >= 30)
    & (customers["city"] == "서울")
]
```

각 조건은 괄호로 묶는 것이 중요하다.

## 3. `isin()`

여러 값 중 하나에 해당하는지 확인할 때 편하다.

```python
customers[
    customers["city"].isin(["서울", "부산"])
]
```

쉽게 읽으면:

```text
city가 [서울, 부산] 안에 있냐?
```

SQL의 `IN`과 비슷하다.

반대로 특정 값들을 제외하려면 `~`를 붙인다.

```python
orders[
    ~orders["order_status"].isin([
        "cancelled",
        "refunded"
    ])
]
```

## 4. 필터 결과가 아무것도 안 나올 때

코드가 틀렸다고 바로 생각하지 말고 실제 값을 먼저 확인한다.

```python
print(customers["city"].value_counts(dropna=False))
```

확인할 것:

```text
서울인지 Seoul인지
앞뒤 공백이 있는지
대소문자가 다른지
결측치인지
원하는 값이 실제로 존재하는지
```

특히 `isin()`은 실제 값과 정확하게 맞아야 한다.

## 5. 결측치란?

결측치는 값이 비어 있는 상태다.

pandas에서는 주로 `NaN`, `None`, `pd.NA` 같은 형태로 나타난다.

결측치 확인:

```python
df.isna()
```

각 칸이 비었는지 `True`, `False`로 보여준다.

하지만 실제로는 보통 개수를 보고 싶기 때문에 다음처럼 많이 쓴다.

```python
df.isna().sum()
```

## 6. `isna().sum()`은 어떻게 읽나?

```text
df
↓
isna()
↓
비어 있으면 True
↓
sum()
↓
True를 1처럼 세서 개수 계산
```

예:

```python
customers["age"].isna().sum()
```

이 코드는 `age` 컬럼의 결측치 개수를 센다.

DataFrame 전체에 사용하면 컬럼별 결측치 개수가 나온다.

```python
customers.isna().sum()
```

## 7. 전체 결측치 개수까지 보고 싶으면

```python
customers.isna().sum().sum()
```

첫 번째 `sum()`은 컬럼별 결측치 수를 계산하고,
두 번째 `sum()`은 그 숫자들을 다시 모두 더한다.

## 8. 결측치가 0이어도 의미가 있다

```python
print(customers.isna().sum())
```

모두 0이 나왔다면 아무 일도 없다는 뜻이 아니라,

```text
현재 확인한 데이터에서는 결측치가 발견되지 않았다
```

라는 분석 결과다.

## 9. 빈 문자열과 결측치는 다르다

```python
""
```

이 값은 빈 문자열이지 자동으로 결측치가 되는 것은 아니다.

공백만 들어 있는 값도 마찬가지다.

```python
"   "
```

그래서 문자열 정리 후 빈 문자열을 `pd.NA`로 바꾸기도 한다.

```python
df["city"] = df["city"].str.strip()
df["city"] = df["city"].replace("", pd.NA)
```

## 10. 가장 먼저 기억할 패턴

```python
print(df.columns.tolist())
print(df.dtypes)
print(df.shape)
print(df.isna().sum())
```

필터가 이상하면:

```python
print(df["컬럼명"].value_counts(dropna=False))
```

이 정도만 먼저 확인해도 상당수 오류 원인을 찾을 수 있다.

## 정리

```text
조건식 → True / False
DataFrame[조건식] → 조건에 맞는 행
isin() → 여러 값 중 하나인지 확인
~isin() → 해당 값들 제외
isna() → 결측 여부
isna().sum() → 결측 개수
value_counts() → 실제 값 분포 확인
```
