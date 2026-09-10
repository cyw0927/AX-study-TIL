# 14. pandas groupby와 집계

데이터 분석에서는 전체 합계만 보는 것보다 **그룹별로 나누어 보는 것**이 훨씬 중요하다.

예를 들어 전체 매출이 아니라 카테고리별 매출, 월별 매출, 고객별 구매금액을 알고 싶을 때 `groupby()`를 사용한다.

## 1. 가장 기본적인 groupby

```python
products.groupby("category")["price"].mean()
```

읽는 순서:

```text
products에서
↓
category 기준으로 묶고
↓
price 컬럼을 보고
↓
평균을 계산한다
```

## 2. groupby에서 가장 중요한 것

`groupby()`의 기준 컬럼은 **결과 한 행이 무엇을 의미하는지 결정한다.**

```text
groupby("category")
→ 결과 한 행 = 카테고리 하나

groupby("customer_id")
→ 결과 한 행 = 고객 한 명

groupby("order_month")
→ 결과 한 행 = 한 달
```

그래서 코드를 보기 전에 먼저 질문해야 한다.

```text
나는 무엇을 기준으로 묶고 싶은가?
```

## 3. 여러 계산을 한 번에: agg()

```python
summary = (
    products
    .groupby("category", as_index=False)
    .agg(
        product_count=("product_id", "nunique"),
        average_price=("price", "mean"),
        minimum_price=("price", "min"),
        maximum_price=("price", "max")
    )
)
```

`agg()`는 여러 집계값을 한 번에 만들 때 사용한다.

## 4. as_index=False

```python
.groupby("category", as_index=False)
```

이 옵션을 쓰면 `category`가 index로 빠지지 않고 일반 컬럼으로 유지된다.

초보 입장에서는 결과를 표처럼 보기 편하고, 이후 저장이나 병합에도 편하다.

## 5. count(), size(), nunique()

셋은 비슷해 보이지만 의미가 다르다.

```text
count()
→ 결측치를 제외한 값 개수

size()
→ 전체 행 개수

nunique()
→ 서로 다른 값 개수
```

예를 들어 주문상세 데이터에서:

```python
len(order_items)
```

이 값은 주문상세 행 수다.

하지만 실제 주문 건수를 알고 싶다면:

```python
order_items["order_id"].nunique()
```

를 사용해야 한다.

한 주문에 여러 상품이 들어갈 수 있기 때문이다.

## 6. 매출 집계 예시

주문상세 한 행의 금액을 먼저 만든다.

```python
order_items["line_total"] = (
    order_items["quantity"]
    * order_items["unit_price"]
)
```

그 다음 카테고리별 매출을 구한다고 가정하면:

```python
category_sales = (
    completed_items
    .groupby("category", as_index=False)
    .agg(
        total_sales=("line_total", "sum"),
        order_count=("order_id", "nunique"),
        customer_count=("customer_id", "nunique"),
        quantity_sold=("quantity", "sum")
    )
)
```

이 결과에서 한 행은 카테고리 하나다.

## 7. 판매량 1위와 매출 1위는 다를 수 있다

```text
quantity_sold
→ 몇 개 팔렸는가

total_sales
→ 얼마를 벌었는가
```

가격이 싼 상품이 많이 팔릴 수도 있고,
가격이 비싼 상품이 적게 팔려도 매출은 더 클 수 있다.

그래서 "가장 잘 팔린 상품"이라는 표현은 애매하다.

```text
판매량 기준인지
매출 기준인지
주문 수 기준인지
```

먼저 기준을 정해야 한다.

## 8. 집계 후 검증

그룹별 결과를 만들었다면 전체 합계와 맞는지 확인한다.

```python
category_total = category_sales["total_sales"].sum()
source_total = completed_items["line_total"].sum()

print(category_total)
print(source_total)
print(category_total == source_total)
```

합계가 다르면 다음을 의심할 수 있다.

```text
결측 카테고리가 있는가?
병합 과정에서 행이 늘었는가?
필터 범위가 다른가?
미매칭 데이터가 있는가?
```

## 9. 초보용 읽는 법

```python
df.groupby("A")["B"].sum()
```

이 코드를 한 번에 외우지 말고:

```text
df
→ A로 묶고
→ B만 보고
→ 합계를 계산한다
```

이렇게 읽는다.

## 정리

```text
groupby() → 무엇을 기준으로 묶을지 정함
agg() → 여러 집계값 계산
sum() → 합계
mean() → 평균
count() → 결측 제외 개수
size() → 전체 행 수
nunique() → 고유값 개수
```

가장 중요한 것은 함수 이름보다 **결과 한 행이 무엇을 의미하는지 이해하는 것**이다.
