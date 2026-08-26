# SELECT 연습

SQL에서 가장 먼저 많이 쓰는 명령은 `SELECT`다.

쉽게 말하면 데이터베이스에게 **"이 자료 좀 보여줘"**라고 말하는 명령이다.

## 전체 보기

```sql
SELECT * FROM students;
```

뜻:

- `SELECT` → 보여줘
- `*` → 모든 열을
- `FROM students` → students 테이블에서

## 원하는 열만 보기

```sql
SELECT name, score FROM students;
```

이름과 점수 열만 본다.

## 조건 걸기

```sql
SELECT * FROM students
WHERE score >= 80;
```

점수가 80 이상인 행만 가져온다.

## 문자열 조건

```sql
SELECT * FROM students
WHERE name = '철수';
```

SQL에서는 문자열을 보통 따옴표로 감싼다.

## 여러 조건

```sql
SELECT * FROM students
WHERE score >= 80 AND age >= 20;
```

두 조건을 모두 만족해야 한다.

```sql
SELECT * FROM students
WHERE score >= 90 OR age <= 19;
```

둘 중 하나만 만족해도 된다.

## 정렬

```sql
SELECT * FROM students
ORDER BY score DESC;
```

점수가 높은 순서로 정렬한다.

```sql
ORDER BY score ASC;
```

낮은 순서다.

## 개수 세기

```sql
SELECT COUNT(*) FROM students;
```

행이 몇 개인지 센다.

## 평균 구하기

```sql
SELECT AVG(score) FROM students;
```

점수 평균을 구한다.

## Python이랑 비슷하게 생각하기

Python에서는 이런 식으로 조건을 건다.

```python
if score >= 80:
    print(name)
```

SQL에서는:

```sql
SELECT name FROM students
WHERE score >= 80;
```

문법은 다르지만 결국 **조건에 맞는 데이터를 골라내는 것**이라는 점은 비슷하다.

## 연습

students 테이블에 `name`, `age`, `score`가 있다고 생각하고 다음을 직접 작성해 본다.

1. 전체 데이터 보기
2. 이름만 보기
3. 점수 70 이상 보기
4. 나이 20 이상이면서 점수 80 이상 보기
5. 점수 높은 순으로 보기
6. 전체 학생 수 세기
7. 평균 점수 구하기

처음에는 SQL을 외우기보다 `SELECT → FROM → WHERE → ORDER BY` 순서가 자주 나온다는 것부터 익히면 된다.
