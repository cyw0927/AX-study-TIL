# HTML과 CSS 진짜 기초

웹페이지를 처음 보면 Python과 완전히 다른 세계처럼 보일 수 있다. 그런데 역할만 나누면 어렵지 않다.

## HTML은 뼈대

HTML은 웹페이지에 무엇이 있는지 적는다.

```html
<h1>안녕하세요</h1>
<p>첫 웹페이지입니다.</p>
<button>누르기</button>
```

쉽게 말하면:

- `h1` → 큰 제목
- `p` → 문단
- `button` → 버튼

HTML은 "여기에 제목이 있고, 여기에 문장이 있고, 여기에 버튼이 있다"를 적는 것이다.

## CSS는 꾸미기

CSS는 HTML의 모양을 바꾼다.

```css
h1 {
    font-size: 30px;
}
```

이 코드는 `h1` 제목 글씨 크기를 바꾼다.

HTML이 집의 벽과 문이라면 CSS는 벽지, 색깔, 크기, 간격을 꾸미는 역할이라고 생각하면 된다.

## 태그가 뭐지?

HTML에서는 이런 모양을 자주 본다.

```html
<p>안녕</p>
```

`<p>`는 시작 태그, `</p>`는 끝 태그다.

그 사이의 `안녕`이 실제 내용이다.

## 속성은 뭐지?

```html
<a href="https://example.com">사이트</a>
```

`href`는 링크 주소를 적는 속성이다.

```html
<img src="cat.jpg">
```

`src`는 이미지 파일 위치를 적는다.

## id와 class

CSS에서 특정 요소를 골라 꾸밀 때 자주 쓴다.

```html
<p id="title">제목</p>
<p class="item">짜장면</p>
<p class="item">짬뽕</p>
```

- `id`는 보통 하나를 딱 가리킬 때
- `class`는 여러 개를 같은 그룹으로 묶을 때

사용한다.

## 직접 해보기

아래 내용을 `index.html`로 저장하고 브라우저에서 열어 본다.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>내 첫 페이지</title>
</head>
<body>
    <h1>안녕하세요</h1>
    <p>HTML 연습 중입니다.</p>
</body>
</html>
```

처음에는 모든 태그를 외우려고 하지 말고, 제목 하나와 문장 하나가 화면에 뜨는지만 확인하면 된다.
