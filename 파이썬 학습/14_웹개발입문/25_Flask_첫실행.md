# Flask 첫 실행

Flask는 Python으로 간단한 웹서버를 만들 때 많이 쓰는 도구다.

## 먼저 설치

터미널에서:

```bash
pip install flask
```

Python 코드 안에 쓰는 명령이 아니라 터미널에서 실행하는 명령이다.

## 가장 작은 Flask 코드

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "안녕하세요"

app.run(debug=True)
```

처음 보면 이상한 기호가 많지만 한 줄씩 보면 된다.

## `from flask import Flask`

Flask라는 도구를 가져온다.

## `app = Flask(__name__)`

웹 프로그램 하나를 만든다.

지금 단계에서는 `__name__`을 완벽히 이해하지 않아도 된다. Flask가 현재 파일을 기준으로 앱을 만들 때 사용하는 값이라고 생각하면 된다.

## `@app.route("/")`

브라우저가 `/` 주소로 들어왔을 때 바로 아래 함수를 실행하라는 뜻이다.

```python
@app.route("/")
def home():
    return "안녕하세요"
```

브라우저가 첫 화면을 요청하면 `home()` 함수가 실행되고 문자열을 돌려준다.

## 서버를 실행하면 왜 프로그램이 안 끝나지?

```python
app.run(debug=True)
```

웹서버는 한 번 실행하고 끝나는 프로그램이 아니다.

브라우저가 언제 요청할지 모르기 때문에 계속 기다린다.

그래서 터미널이 멈춘 것처럼 보여도 정상일 수 있다.

## localhost는 뭐지?

`localhost`는 현재 내 컴퓨터를 뜻한다.

예:

```text
http://127.0.0.1:5000
```

보통 Flask 기본 포트는 5000이다.

## 종료하는 방법

터미널에서 보통 `Ctrl + C`를 누르면 서버가 종료된다.

## 초보가 많이 헷갈리는 것

### Python 파일 이름을 `flask.py`로 만들지 않기

내 파일 이름이 Flask 라이브러리 이름과 겹치면 import가 꼬일 수 있다.

예:

```text
app.py
main.py
```

처럼 짓는 편이 안전하다.

### 브라우저 주소와 파일 경로는 다르다

`/hello`는 Windows 폴더 경로가 아니라 웹 주소의 일부다.

## 한 단계 더

```python
@app.route("/hello")
def hello():
    return "hello 페이지"
```

이제 브라우저에서 `/hello`로 들어가면 다른 문장이 나온다.

처음에는 라우트 하나를 추가하고 화면이 바뀌는 것만 확인하면 충분하다.
