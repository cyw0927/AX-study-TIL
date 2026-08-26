# 27. INSERT, UPDATE, DELETE 기초

SQL에서 `SELECT`가 데이터를 조회하는 명령이라면, `INSERT`, `UPDATE`, `DELETE`는 데이터를 직접 바꾸는 명령이다.

처음에는 세 개를 이렇게 기억하면 된다.

```text
INSERT → 새 데이터 추가
UPDATE → 기존 데이터 수정
DELETE → 기존 데이터 삭제
```

## INSERT

새 행을 추가한다.

```sql
INSERT INTO students (name, score)
VALUES ('철수', 90);
```

뜻은:

```text
students 테이블에
name='철수'
score=90
인 새 행을 추가한다.
```

## 여러 개 추가

```sql
INSERT INTO students (name, score)
VALUES
('철수', 90),
('영희', 85),
('민수', 70);
```

## UPDATE

기존 데이터를 수정한다.

```sql
UPDATE students
SET score = 95
WHERE name = '철수';
```

뜻:

```text
students 테이블에서
name이 철수인 행을 찾아서
score를 95로 바꾼다.
```

## WHERE가 정말 중요하다

다음 코드는 매우 위험하다.

```sql
UPDATE students
SET score = 0;
```

`WHERE`가 없으므로 **모든 학생의 score가 0으로 바뀔 수 있다.**

그래서 수정 전에는 먼저 같은 조건으로 조회해 보는 습관이 좋다.

```sql
SELECT * FROM students
WHERE name = '철수';
```

원하는 행만 나오는지 확인한 뒤 `UPDATE`를 실행한다.

## DELETE

행을 삭제한다.

```sql
DELETE FROM students
WHERE name = '민수';
```

민수의 행을 삭제한다.

## DELETE도 WHERE 주의

```sql
DELETE FROM students;
```

이 코드는 조건이 없어서 테이블 안의 모든 행을 삭제할 수 있다.

초보 단계에서는 `UPDATE`, `DELETE`를 실행하기 전에 항상 이렇게 생각한다.

```text
1. WHERE 조건이 있는가?
2. SELECT로 먼저 대상 행을 확인했는가?
3. 정말 그 데이터만 바꾸거나 지우는가?
```

## Python SQLite에서 INSERT

```python
import sqlite3

conn = sqlite3.connect("school.db")
cursor = conn.cursor()

cursor.execute(
    "INSERT INTO students (name, score) VALUES (?, ?)",
    ("철수", 90)
)

conn.commit()
conn.close()
```

## `commit()`은 왜 필요한가?

데이터를 추가하거나 수정하거나 삭제한 내용을 실제 DB 파일에 저장하려면 `commit()`이 필요하다.

```text
execute() → 변경 작업 실행
commit()  → 변경 내용 확정
```

## `?`는 왜 쓰나?

```python
cursor.execute(
    "INSERT INTO students (name, score) VALUES (?, ?)",
    (name, score)
)
```

문자열을 직접 이어 붙이기보다 값을 따로 전달하는 방식이다.

초보 단계에서는 **SQL 문자열 안에 변수값을 억지로 붙이지 말고 `?`를 사용한다**고 기억하면 된다.

## UPDATE 예제

```python
cursor.execute(
    "UPDATE students SET score = ? WHERE name = ?",
    (95, "철수")
)
conn.commit()
```

## DELETE 예제

```python
cursor.execute(
    "DELETE FROM students WHERE name = ?",
    ("민수",)
)
conn.commit()
```

값이 하나뿐인 튜플은 `(값,)`처럼 쉼표가 필요하다.

## 직접 연습

1. 학생 한 명 추가
2. 학생 점수 수정
3. 학생 한 명 삭제
4. 각 작업 전에 `SELECT`로 대상 확인
5. 작업 후 다시 `SELECT`해서 실제로 바뀌었는지 확인

SQL에서 데이터를 바꾸는 명령은 강력하기 때문에 **조회 → 확인 → 수정/삭제 → 다시 조회** 순서를 습관으로 만드는 것이 좋다.
