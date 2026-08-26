# 실제 CSV 파일을 처음 분석할 때 순서

CSV 파일을 처음 받으면 바로 `groupby()`부터 쓰기보다 **파일이 어떻게 생겼는지 먼저 확인하는 순서**가 중요하다.

초보자는 아래 순서대로 가면 훨씬 덜 헷갈린다.

## 1. 파일 읽기

```python
import pandas as pd

df = pd.read_csv("orders.csv")
```

`df`는 DataFrame이다. 쉽게 말하면 엑셀 표 같은 데이터다.

## 2. 앞부분 보기

```python
print(df.head())
```

처음 몇 줄을 보여 준다.

여기서 먼저 컬럼 이름과 값 모양을 본다.

## 3. 행과 열 개수 보기

```python
print(df.shape)
```

예를 들어:

```text
(1000, 8)
```

이라면 1000행, 8열이라는 뜻이다.

## 4. 컬럼 이름 보기

```python
print(df.columns)
```

컬럼명을 잘못 알고 있으면 뒤에서 계속 `KeyError`가 날 수 있다.

## 5. 자료형 보기

```python
print(df.dtypes)
```

숫자인 줄 알았는데 문자열로 들어온 경우가 많다.

예:

```text
price     object
count      int64
```

`price`가 `object`라면 계산 전에 확인이 필요하다.

## 6. 빈 값 보기

```python
print(df.isna().sum())
```

각 컬럼에 빈 값이 몇 개인지 확인한다.

## 7. 중복 확인

```python
print(df.duplicated().sum())
```

중복 행이 몇 개인지 본다.

필요하면:

```python
df = df.drop_duplicates()
```

로 제거할 수 있다.

## 8. 숫자 컬럼 기본 통계 보기

```python
print(df.describe())
```

평균, 최솟값, 최댓값 같은 정보를 빠르게 볼 수 있다.

## 9. 필요한 계산 컬럼 만들기

예를 들어 가격과 수량이 있다면:

```python
df["amount"] = df["price"] * df["count"]
```

새 컬럼을 만든다.

## 10. 조건으로 필요한 데이터만 보기

```python
completed = df[df["status"] == "완료"]
```

특정 상태만 보고 싶을 때 쓴다.

## 11. 그룹별로 묶어 보기

```python
category_sales = df.groupby("category")["amount"].sum()
print(category_sales)
```

카테고리별 매출 합계처럼 묶어서 볼 수 있다.

## 12. 정렬하기

```python
category_sales = category_sales.sort_values(ascending=False)
print(category_sales)
```

큰 값부터 볼 수 있다.

## 분석 순서를 한 줄로 기억하기

```text
읽기
→ 모양 보기
→ 컬럼 확인
→ 자료형 확인
→ 빈 값 확인
→ 중복 확인
→ 필요한 계산
→ 필터
→ groupby
→ 정렬
→ 해석
```

## 중요한 점: 분석은 숫자 출력으로 끝나지 않는다

예를 들어 결과가:

```text
전자제품  5000000
식품      2000000
의류      1500000
```

이라고 나왔다면 단순히 표를 보여 주는 것으로 끝내지 말고:

```text
전자제품 매출이 가장 높다.
전체 매출에서 전자제품 비중이 큰지 확인할 필요가 있다.
주문 수가 많은 것인지, 주문당 금액이 높은 것인지 추가 확인할 수 있다.
```

처럼 **숫자가 무엇을 의미하는지 한 문장으로 설명하는 단계**가 필요하다.

## 오류가 났을 때 확인 순서

`KeyError`가 나면:

```python
print(df.columns)
```

숫자 계산이 안 되면:

```python
print(df.dtypes)
```

빈 값 때문에 이상하면:

```python
print(df.isna().sum())
```

행 개수가 예상과 다르면:

```python
print(df.shape)
```

을 먼저 본다.

## 직접 연습용 기본 틀

```python
import pandas as pd

df = pd.read_csv("data.csv")

print("앞부분")
print(df.head())

print("크기")
print(df.shape)

print("컬럼")
print(df.columns)

print("자료형")
print(df.dtypes)

print("빈 값")
print(df.isna().sum())
```

처음 보는 CSV라면 일단 이 정도부터 실행한 뒤 다음 분석으로 넘어간다.
