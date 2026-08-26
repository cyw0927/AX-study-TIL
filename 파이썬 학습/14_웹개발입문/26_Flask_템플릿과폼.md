# 26. Flask 템플릿과 폼 입력

Flask로 서버를 켠 다음에는 브라우저에 글자만 보여주는 것보다 HTML 파일을 따로 만들어 연결하는 방법을 배우게 된다.

## 템플릿이란?

템플릿은 쉽게 말하면 **HTML 화면 파일**이다.

Python 코드 안에 HTML을 길게 쓰지 않고, HTML 파일을 따로 두고 Flask가 그 파일을 보여주게 한다.

예를 들어 폴더를 이렇게 만든다.

```text
project/
├─ app.py
└─ templates/
   └─ index.html
```

Flask는 기본적으로 `templates`라는 폴더를 찾는다.

## `render_template()`

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def home():
    return render_template("index.html")
```

`render_template("index.html")`은 `templates/index.html`을 찾아서 브라우저에 보여준다.

## HTML 파일 예제

```html
<!DOCTYPE html>
<html>
<head>
    <title>첫 화면</title>
</head>
<body>
    <h1>안녕하세요</h1>
</body>
</html>
```

여기까지는 Python이 화면 파일을 불러오기만 한 것이다.

## Python 값을 HTML에 보내기

```python
@app.route("/")
def home():
    name = "철수"
    return render_template("index.html", name=name)
```

HTML에서는:

```html
<h1>{{ name }}님 안녕하세요</h1>
```

처럼 쓸 수 있다.

`{{ name }}`은 Python에서 넘긴 값을 표시하는 자리다.

## 폼(form)이란?

폼은 사용자가 값을 입력해서 서버에 보내는 화면이다.

```html
<form method="post">
    <input type="text" name="username">
    <button type="submit">보내기</button>
</form>
```

여기서 중요한 것은 `name="username"`이다.

서버는 이 이름을 사용해서 값을 꺼낸다.

## Flask에서 입력값 받기

```python
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route("/", methods=["GET", "POST"])
def home():
    if request.method == "POST":
        username = request.form["username"]
        return f"입력한 이름: {username}"

    return render_template("index.html")
```

흐름은 다음과 같다.

```text
브라우저에서 이름 입력
→ 제출 버튼 클릭
→ 서버로 POST 요청
→ Flask가 request.form에서 값 확인
→ 결과를 다시 브라우저에 보여줌
```

## GET과 POST를 아주 쉽게 구분하면

- GET: 페이지를 보여 달라고 요청
- POST: 사용자가 입력한 데이터를 서버로 보냄

처음에는 이 정도로 이해하면 충분하다.

## 초보가 자주 헷갈리는 부분

### `request.form["username"]`의 username은 어디서 왔나?

HTML의 이 부분과 연결된다.

```html
<input name="username">
```

### `templates` 폴더 이름을 마음대로 바꿔도 되나?

처음에는 바꾸지 않는 것이 좋다. Flask의 기본 규칙을 그대로 사용하는 것이 덜 헷갈린다.

### HTML과 Python은 같은 언어인가?

아니다.

Python은 서버에서 실행되고 HTML은 브라우저 화면의 구조를 만든다.

## 직접 연습

1. 이름 입력창 만들기
2. POST로 서버에 보내기
3. Flask에서 입력값 받기
4. 받은 이름을 화면에 출력하기

이 네 단계만 성공하면 Flask에서 가장 기본적인 입력 흐름을 이해한 것이다.
