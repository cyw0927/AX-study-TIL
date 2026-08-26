# 24. SQL이 뭔가요?

SQL은 데이터베이스에 있는 데이터를 찾고, 추가하고, 바꾸고, 지울 때 사용하는 언어다.

Python하고는 다른 언어지만 데이터 분석이나 웹개발을 하다 보면 자주 같이 쓴다.

## 데이터베이스를 아주 쉽게 생각하면

엑셀 표가 엄청 많이 모여 있고, 여러 프로그램이 같이 쓰는 저장소라고 생각하면 된다.

예를 들어 회원 정보가 이렇게 저장되어 있다고 하자.

| id | name | age |
|---:|---|---:|
| 1 | 철수 | 20 |
| 2 | 영희 | 25 |
| 3 | 민수 | 30 |

이런 표를 데이터베이스에서는 보통 **테이블(table)**이라고 부른다.

## 자주 나오는 말

```text
database = 데이터 저장소
 table   = 표
 row     = 한 줄
 column  = 한 열
```

예를 들어 `name`은 열이고, `철수 / 20` 같은 한 사람의 정보는 한 행에 들어간다.

## SELECT

데이터를 조회할 때 쓴다.

```sql
SELECT * FROM users;
```

쉽게 읽으면:

```text
users 테이블에서
모든 열(*)을
보여줘
```

## 특정 열만 보기

```sql
SELECT name, age FROM users;
```

이러면 이름과 나이만 가져온다.

## WHERE

조건을 붙일 때 쓴다.

```sql
SELECT *
FROM users
WHERE age >= 25;
```

뜻은:

```text
users에서
나이가 25 이상인 사람만 보여줘
```

Python의 `if`와 완전히 같지는 않지만, 초보 단계에서는 **조건을 거는 역할**이라고 생각하면 된다.

## ORDER BY

정렬할 때 쓴다.

```sql
SELECT *
FROM users
ORDER BY age DESC;
```

`DESC`는 큰 값부터, `ASC`는 작은 값부터 정렬한다.

## INSERT

새 데이터를 추가한다.

```sql
INSERT INTO users (name, age)
VALUES ('민지', 22);
```

회원 한 명을 새로 넣는 느낌이다.

## UPDATE

기존 데이터를 수정한다.

```sql
UPDATE users
SET age = 26
WHERE name = '영희';
```

여기서 `WHERE`를 빼면 여러 행이 한꺼번에 바뀔 수 있어서 특히 조심해야 한다.

## DELETE

데이터를 삭제한다.

```sql
DELETE FROM users
WHERE name = '민수';
```

역시 `WHERE`가 매우 중요하다.

## Python과 SQL은 어떻게 같이 쓰나?

Python 프로그램이 데이터베이스에 SQL을 보내서 데이터를 가져오는 식으로 많이 쓴다.

```text
Python 프로그램
   ↓ SQL 요청
데이터베이스
   ↓ 결과
Python 프로그램
```

예를 들어 웹사이트에서 "내 주문 목록" 버튼을 누르면 서버의 Python 코드가 데이터베이스에 주문 정보를 요청할 수 있다.

## pandas하고 느낌 비교

SQL:

```sql
SELECT * FROM users WHERE age >= 25;
```

pandas:

```python
result = df[df["age"] >= 25]
```

둘 다 결국 "조건에 맞는 데이터만 뽑기"를 하는 것이다.

## 처음에는 이것만 기억

```text
SELECT   = 보기
WHERE    = 조건
ORDER BY = 정렬
INSERT   = 추가
UPDATE   = 수정
DELETE   = 삭제
```

SQL은 문법을 전부 외우는 것보다 작은 표를 만들어 놓고 조회문을 직접 여러 번 써 보는 게 훨씬 이해하기 쉽다.
