# Python과 SQLite 첫걸음

SQLite는 별도 서버를 크게 준비하지 않아도 파일 하나로 사용할 수 있는 작은 데이터베이스다.

Python에는 `sqlite3`가 기본으로 들어 있어서 따로 설치하지 않아도 사용할 수 있다.

## 연결하기

```python
import sqlite3

conn = sqlite3.connect("study.db")
```

`study.db`라는 데이터베이스 파일에 연결한다. 파일이 없으면 새로 만들어질 수 있다.

## cursor가 뭐지?

```python
cursor = conn.cursor()
```

SQL 명령을 보내는 데 사용하는 도구라고 생각하면 된다.

## 테이블 만들기

```python
cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    name TEXT,
    score INTEGER
)
""")
```

처음에는 SQL이 문자열 안에 들어간다는 점만 이해하면 된다.

## 데이터 넣기

```python
cursor.execute(
    "INSERT INTO students (name, score) VALUES (?, ?)",
    ("철수", 90)
)
```

`?` 자리에 실제 값이 들어간다.

문자열을 직접 이어 붙이는 것보다 이런 방식이 안전하다.

## 저장하기

```python
conn.commit()
```

데이터를 변경한 내용을 실제로 저장한다.

## 데이터 읽기

```python
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()

for row in rows:
    print(row)
```

`fetchall()`은 조회 결과를 전부 가져온다.

## 연결 닫기

```python
conn.close()
```

사용이 끝나면 닫아준다.

## 전체 흐름

```text
연결
↓
cursor 만들기
↓
SQL 실행
↓
필요하면 commit
↓
결과 읽기
↓
연결 닫기
```

## 아주 작은 전체 예제

```python
import sqlite3

conn = sqlite3.connect("study.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    name TEXT,
    score INTEGER
)
""")

cursor.execute(
    "INSERT INTO students (name, score) VALUES (?, ?)",
    ("영희", 85)
)

conn.commit()

cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()

for row in rows:
    print(row)

conn.close()
```

처음에는 이 코드를 외우려고 하지 말고 "Python이 SQL 문장을 데이터베이스에 보내는구나" 정도로 이해하면 된다.
