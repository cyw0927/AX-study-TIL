# 28. Flask와 데이터베이스 연결 기초

웹사이트에서 회원, 게시글, 점수 같은 정보를 계속 기억하려면 데이터베이스가 필요하다.

## 왜 변수만 쓰면 안 될까?

```python
users = ["철수", "영희"]
```

이렇게 변수에만 저장하면 프로그램이 종료될 때 값이 사라질 수 있다.

데이터베이스는 프로그램을 껐다 켜도 데이터를 보관하는 역할을 한다.

## 초보 연습에는 SQLite가 편하다

SQLite는 별도 서버를 설치하지 않고 파일 하나로 사용할 수 있다.

```python
import sqlite3

conn = sqlite3.connect("app.db")
```

`app.db`라는 데이터베이스 파일에 연결한다.

## 테이블 만들기

```python
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT
)
""")

conn.commit()
```

## 데이터 넣기

```python
cursor.execute(
    "INSERT INTO users (name) VALUES (?)",
    ("철수",)
)
conn.commit()
```

`?` 자리에 실제 값이 들어간다.

문자열을 SQL 문장에 직접 이어 붙이는 것보다 이런 방식이 안전하다.

## 데이터 읽기

```python
cursor.execute("SELECT * FROM users")
rows = cursor.fetchall()

print(rows)
```

## Flask와 연결하면

큰 흐름은 이렇다.

```text
브라우저
↓ 요청
Flask
↓ SQL 실행
SQLite
↓ 결과
Flask
↓ HTML로 보여주기
브라우저
```

## 아주 작은 예제

```python
from flask import Flask
import sqlite3

app = Flask(__name__)

@app.route("/users")
def users():
    conn = sqlite3.connect("app.db")
    cursor = conn.cursor()
    cursor.execute("SELECT name FROM users")
    rows = cursor.fetchall()
    conn.close()

    return str(rows)
```

실제 웹페이지에서는 `str(rows)` 대신 템플릿으로 넘겨서 HTML로 보여주는 경우가 많다.

## 연결을 닫는 이유

```python
conn.close()
```

데이터베이스를 사용한 뒤 연결을 정리한다.

## 초보 단계에서 기억할 것

```text
Flask = 요청을 받고 처리하는 웹 서버 쪽 코드
SQLite = 데이터를 저장하는 곳
SQL = 데이터베이스에 명령을 내리는 언어
```

이 세 가지가 연결되면 회원가입, 로그인, 게시판 같은 기능을 만들 수 있다.
