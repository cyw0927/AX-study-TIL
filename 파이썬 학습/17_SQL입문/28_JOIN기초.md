# 28. JOIN 기초

`JOIN`은 **서로 다른 테이블의 데이터를 연결해서 같이 보는 방법**이다.

처음 보면 어려워 보이지만 핵심은 간단하다.

> 두 표에서 서로 연결되는 공통 번호를 찾아 합쳐서 본다.

## 예시 테이블 1: students

| id | name |
|---|---|
| 1 | 철수 |
| 2 | 영희 |

## 예시 테이블 2: scores

| student_id | score |
|---|---|
| 1 | 90 |
| 2 | 85 |

`students.id`와 `scores.student_id`가 서로 연결되는 값이다.

## INNER JOIN

```sql
SELECT students.name, scores.score
FROM students
INNER JOIN scores
ON students.id = scores.student_id;
```

결과는 이런 느낌이다.

| name | score |
|---|---|
| 철수 | 90 |
| 영희 | 85 |

## 한 줄씩 읽기

```sql
SELECT students.name, scores.score
```

두 테이블에서 어떤 열을 보여줄지 정한다.

```sql
FROM students
```

students 테이블을 기준으로 시작한다.

```sql
INNER JOIN scores
```

scores 테이블도 연결한다.

```sql
ON students.id = scores.student_id
```

어떤 값이 서로 같을 때 연결할지 정한다.

## 왜 테이블을 나눌까?

모든 정보를 한 표에 몰아넣는 것보다 역할별로 나누는 경우가 많다.

예:

```text
users       → 사용자 정보
orders      → 주문 정보
products    → 상품 정보
```

주문 테이블에 사용자 이름과 상품 이름을 계속 복사해서 넣기보다, 사용자 번호와 상품 번호를 저장하고 필요할 때 JOIN으로 연결할 수 있다.

## LEFT JOIN

`LEFT JOIN`은 왼쪽 테이블의 데이터는 모두 보여주고, 오른쪽에서 연결되는 데이터가 있으면 붙인다.

```sql
SELECT students.name, scores.score
FROM students
LEFT JOIN scores
ON students.id = scores.student_id;
```

예를 들어 영희의 점수가 아직 없어도 영희 자체는 결과에 남을 수 있다.

점수가 없으면 보통 `NULL`로 나타난다.

## INNER JOIN과 LEFT JOIN 아주 간단히

```text
INNER JOIN
→ 양쪽에 연결되는 데이터만

LEFT JOIN
→ 왼쪽 데이터는 전부 유지
```

## 별칭(alias)

테이블 이름이 길면 줄여 쓸 수 있다.

```sql
SELECT s.name, sc.score
FROM students AS s
JOIN scores AS sc
ON s.id = sc.student_id;
```

여기서:

```text
s  → students
sc → scores
```

처음에는 별칭 없이 이해한 뒤 나중에 써도 된다.

## 초보가 자주 헷갈리는 부분

### `ON`은 뭐지?

두 테이블을 어떤 조건으로 연결할지 적는 부분이다.

### `WHERE`와 `ON`은 같은 건가?

아니다.

- `ON`: 테이블끼리 어떻게 연결할지
- `WHERE`: 연결한 결과에서 어떤 행만 볼지

예:

```sql
SELECT s.name, sc.score
FROM students AS s
JOIN scores AS sc
ON s.id = sc.student_id
WHERE sc.score >= 90;
```

## 직접 연습

1. 학생 테이블과 점수 테이블 만들기
2. `student_id`로 연결하기
3. 이름과 점수 함께 출력하기
4. INNER JOIN 결과 확인하기
5. LEFT JOIN으로 바꾸고 차이 확인하기
6. WHERE를 붙여 90점 이상만 보기

JOIN은 처음부터 외우기보다 **두 표를 종이에 그려 놓고 어떤 번호끼리 연결되는지 선을 그어보는 방식**으로 이해하면 훨씬 쉽다.
