# 15. pandas 데이터 병합 merge

실제 데이터는 한 파일에 모든 정보가 들어 있지 않은 경우가 많다.

예를 들어 쇼핑몰 데이터에서는:

```text
orders
→ 주문 상태, 주문 날짜, 고객 번호

order_items
→ 어떤 상품을 몇 개 샀는지, 단가가 얼마인지

products
→ 상품명, 카테고리

customers
→ 고객의 성별, 나이, 지역
```

이렇게 정보가 나뉘어 있을 수 있다.

이 데이터를 연결할 때 `merge()`를 사용한다.

## 1. 가장 기본적인 merge

```python
result = order_items.merge(
    orders,
    on="order_id",
    how="left"
)
```

읽으면:

```text
order_items를 기준으로
orders를
order_id가 같은 것끼리
left 방식으로 붙인다
```

## 2. on은 연결 기준

```python
on="order_id"
```

두 DataFrame에서 같은 의미를 가진 키를 기준으로 연결한다.

키를 잘못 선택하면 코드가 실행되더라도 잘못된 결과가 나올 수 있다.

## 3. merge 방식

```text
left
→ 왼쪽 DataFrame의 행을 모두 유지

right
→ 오른쪽 DataFrame의 행을 모두 유지

inner
→ 양쪽에 모두 존재하는 키만 유지

outer
→ 양쪽의 모든 키를 유지
```

처음에는 `left`와 `inner`의 차이를 먼저 이해하면 된다.

## 4. left merge도 행 수가 늘어날 수 있다

초보 때 가장 헷갈리기 쉬운 부분이다.

`left`라고 해서 왼쪽 행 수가 항상 그대로 유지되는 것은 아니다.

예를 들어 오른쪽 DataFrame에 같은 `order_id`가 두 번 있다면:

```text
왼쪽 1행
↓
오른쪽 2행과 각각 연결
↓
결과 2행
```

그래서 병합 전후 행 수를 비교해야 한다.

```python
print("병합 전:", len(order_items))
print("병합 후:", len(result))
```

## 5. 관계 이해하기

대표적인 관계:

```text
1:1
→ 양쪽 키가 모두 고유

1:N
→ 왼쪽 하나가 오른쪽 여러 행과 연결

N:1
→ 왼쪽 여러 행이 오른쪽 하나와 연결

N:M
→ 양쪽 모두 키가 반복
```

예:

```text
order_items.order_id
→ 같은 주문에 여러 상품이 있으므로 반복 가능

orders.order_id
→ 주문 한 건당 하나이므로 고유해야 함
```

따라서:

```text
order_items → orders
N:1 관계
```

## 6. validate로 관계 검증

```python
result = order_items.merge(
    orders,
    on="order_id",
    how="left",
    validate="many_to_one"
)
```

`many_to_one`은:

```text
왼쪽 키 반복 가능
오른쪽 키는 고유해야 함
```

이라는 뜻이다.

오른쪽 키가 중복되어 있으면 오류를 내서 잘못된 병합을 빨리 발견할 수 있다.

## 7. indicator로 연결 상태 확인

```python
result = order_items.merge(
    orders,
    on="order_id",
    how="left",
    indicator="order_match"
)
```

이후:

```python
print(result["order_match"].value_counts(dropna=False))
```

대표 값:

```text
both
→ 양쪽에 모두 존재

left_only
→ 왼쪽에는 있지만 오른쪽에는 없음

right_only
→ 오른쪽에만 있음
```

left merge에서는 정상적인 경우 `both`가 대부분 또는 전부여야 한다.

## 8. 병합 전 필요한 컬럼만 고르기

그냥 전체 DataFrame을 붙이면 같은 이름의 컬럼이 겹칠 수 있다.

그러면 `_x`, `_y`가 붙는다.

예:

```text
price_x
price_y
```

그래서 병합 전에 필요한 컬럼만 선택하는 습관이 좋다.

```python
orders_for_merge = orders[
    ["order_id", "customer_id", "order_date", "order_status"]
].copy()
```

## 9. _x, _y가 생겼다면

다음부터 확인한다.

```text
같은 이름 컬럼이 왜 두 개 생겼는가?
둘의 의미가 같은가?
어느 것을 써야 하는가?
병합 전에 필요 없는 컬럼을 제외할 수 있는가?
```

무조건 하나를 지우기보다 의미를 먼저 확인한다.

## 10. 병합 후 검증 체크

```python
print(len(left_df))
print(len(merged_df))
print(merged_df["match"].value_counts(dropna=False))
```

그리고 키 중복도 확인한다.

```python
print(right_df["id"].duplicated().sum())
```

## 11. merge에서 자주 나는 문제

### MergeError

`validate="many_to_one"`인데 오른쪽 키가 중복된 경우 발생할 수 있다.

```python
orders["order_id"].duplicated().sum()
```

으로 확인한다.

### 병합 후 행 수 증가

가능한 원인:

```text
오른쪽 키 중복
잘못된 연결 키
의도하지 않은 N:M 관계
집계 전에 원본 데이터를 그대로 연결
```

### 값이 비어 있음

키가 한쪽에만 존재하는지 `indicator`로 확인한다.

## 정리

```text
merge() → DataFrame 연결
on → 연결 키
how → 연결 방식
validate → 예상 관계 검증
indicator → 연결 성공 여부 확인
```

merge에서 가장 중요한 것은 "붙었다"가 아니라 **제대로 붙었는지 검증하는 것**이다.
