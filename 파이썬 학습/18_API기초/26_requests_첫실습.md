# requests 첫 실습

Python에서 다른 웹서비스에 요청을 보내고 결과를 받을 때 `requests`라는 라이브러리를 많이 쓴다.

## 설치

터미널에서:

```bash
pip install requests
```

Python 코드 안이 아니라 터미널에서 실행한다.

## 가장 기본적인 GET 요청

```python
import requests

response = requests.get("https://example.com")
print(response.status_code)
```

`requests.get()`은 주소에 GET 요청을 보낸다.

## response가 뭐지?

서버가 돌려준 응답을 담고 있는 값이다.

```python
print(type(response))
```

응답 안에는 상태 코드, 본문, 헤더 같은 여러 정보가 들어 있다.

## 상태 코드

```python
print(response.status_code)
```

대표적으로:

```text
200 → 요청 성공
404 → 주소를 찾지 못함
500 → 서버 쪽 오류
```

모든 숫자를 외울 필요는 없다. 처음에는 `200이면 대체로 성공` 정도만 기억해도 된다.

## 글자로 결과 보기

```python
print(response.text)
```

서버가 돌려준 내용을 문자열로 볼 수 있다.

## JSON 응답

API에서는 HTML보다 JSON을 주는 경우가 많다.

```python
response = requests.get("API 주소")
data = response.json()
print(data)
print(type(data))
```

JSON이 Python의 딕셔너리나 리스트 형태로 바뀌어 들어오는 경우가 많다.

## 오류 확인을 먼저 하기

처음에는 다음 순서가 좋다.

```python
response = requests.get("API 주소")

print("상태 코드:", response.status_code)
print("응답 내용:", response.text)
```

바로 복잡한 코드로 넘어가기보다 서버가 실제로 무엇을 돌려주는지 먼저 보는 것이다.

## 파라미터 보내기

```python
params = {
    "page": 1,
    "keyword": "python"
}

response = requests.get("API 주소", params=params)
```

주소 뒤에 검색 조건을 붙여 보내는 방법이다.

## API 키

일부 API는 누가 요청하는지 확인하기 위해 키를 요구한다.

API 키는 비밀번호처럼 공개 저장소에 그대로 올리지 않는 것이 좋다.

## 초보가 자주 만나는 오류

- `ModuleNotFoundError: No module named 'requests'` → requests 설치 여부와 가상환경 확인
- 401 → 인증 정보 문제일 가능성
- 404 → 주소가 잘못됐을 가능성
- JSON 변환 오류 → 실제 응답이 JSON인지 `response.text`로 먼저 확인

## 기억할 흐름

```text
주소 준비
↓
requests.get()
↓
status_code 확인
↓
text 또는 json() 확인
↓
필요한 값 꺼내기
```

처음에는 실제 API를 많이 붙이기보다 이 흐름을 이해하는 것이 중요하다.
