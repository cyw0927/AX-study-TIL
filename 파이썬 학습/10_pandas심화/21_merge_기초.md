# pandas merge 기초

`merge()`는 **서로 다른 두 표를 공통 열을 기준으로 합치는 기능**이다.

엑셀에서 VLOOKUP 비슷한 일을 한다고 생각해도 된다.

## 예제 1: 고객표와 주문표

```python
import pandas as pd

customers = pd.DataFrame({
    "customer_id": [1, 2, 3],
    "name": ["철수", "영희", "민수"]
})

orders = pd.DataFrame({
    "customer_id": [1, 1, 3],
    "price": [10000, 20000, 15000]
})
```

두 표 모두 `customer_id`라는 열을 가지고 있다.

```python
result = pd.merge(customers, orders, on="customer_id")
print(result)
```

`customer_id`가 같은 행끼리 연결된다.

## 왜 merge가 필요한가?

실제 데이터는 한 파일에 모든 정보가 들어 있지 않은 경우가 많다.

예를 들어:

```text
customers.csv → 고객 이름, 성별, 지역
orders.csv    → 주문번호, 고객번호, 주문금액
products.csv  → 상품번호, 상품명, 카테고리
```

분석하려면 이 표들을 연결해야 한다.

## `on=`

```python
pd.merge(customers, orders, on="customer_id")
```

`on`은 **어떤 열을 기준으로 연결할지** 알려준다.

## inner join

기본 `merge()`는 양쪽에 모두 존재하는 값만 남기는 방식이다.

```python
pd.merge(customers, orders, on="customer_id", how="inner")
```

## left join

왼쪽 표의 행은 최대한 유지한다.

```python
pd.merge(customers, orders, on="customer_id", how="left")
```

주문이 없는 고객도 남을 수 있고, 연결할 값이 없으면 `NaN`이 생길 수 있다.

## 초보자가 꼭 확인할 것

merge 전에는 다음을 먼저 본다.

```python
print(customers.columns)
print(orders.columns)
```

그리고 기준 열의 이름과 자료형도 확인한다.

```python
print(customers["customer_id"].dtype)
print(orders["customer_id"].dtype)
```

한쪽은 숫자이고 한쪽은 문자열이면 제대로 연결되지 않을 수 있다.

## 행이 갑자기 늘어날 수도 있다

한 고객이 주문을 여러 번 했다면 고객 한 행이 주문 수만큼 반복될 수 있다.

이건 버그가 아니라 데이터 관계 때문에 생기는 자연스러운 결과일 수 있다.

## 직접 연습

```python
import pandas as pd

students = pd.DataFrame({
    "student_id": [1, 2, 3],
    "name": ["철수", "영희", "민수"]
})

scores = pd.DataFrame({
    "student_id": [1, 3],
    "score": [90, 80]
})

print(pd.merge(students, scores, on="student_id", how="inner"))
print(pd.merge(students, scores, on="student_id", how="left"))
```

두 결과에서 `영희`가 어떻게 달라지는지 확인한다.
