# 28. POST 요청과 API 오류 처리

API에서 `GET`이 데이터를 가져오는 요청이라면 `POST`는 데이터를 서버로 보내는 데 자주 사용한다.

## GET과 POST 다시 비교

```text
GET  → 데이터 주세요
POST → 이 데이터를 받아 주세요
```

실제 API마다 의미가 조금씩 다를 수 있지만 처음에는 이렇게 이해하면 된다.

## `requests.post()`

```python
import requests

url = "https://example.com/api/users"

data = {
    "name": "철수",
    "age": 20
}

response = requests.post(url, json=data)
```

`json=data`는 Python 딕셔너리를 JSON 형태로 보내겠다는 뜻이다.

## 응답 확인

```python
print(response.status_code)
print(response.text)
```

상태 코드를 먼저 보면 요청이 성공했는지 빠르게 확인할 수 있다.

## 자주 보는 상태 코드

```text
200 → 요청 성공
201 → 새 데이터 생성 성공인 경우가 많음
400 → 요청 내용이 잘못됨
401 → 인증이 필요하거나 인증 실패
403 → 권한 없음
404 → 주소나 대상 데이터를 찾을 수 없음
500 → 서버 내부 오류
```

API마다 자세한 의미는 문서를 확인해야 하지만 큰 방향은 이렇게 기억하면 된다.

## 성공했을 때만 JSON 읽기

```python
if response.status_code == 200:
    data = response.json()
    print(data)
else:
    print("요청 실패")
    print(response.status_code)
```

어떤 API는 성공 시 201을 줄 수도 있다.

그래서 다음처럼 범위로 확인하기도 한다.

```python
if 200 <= response.status_code < 300:
    print("성공")
else:
    print("실패")
```

## 네트워크 오류도 생길 수 있다

인터넷이 끊기거나 주소가 잘못되거나 서버가 응답하지 않을 수 있다.

```python
import requests

try:
    response = requests.get("https://example.com", timeout=5)
    print(response.status_code)
except requests.RequestException as e:
    print("요청 중 오류 발생")
    print(e)
```

## `timeout`은 왜 쓰나?

```python
requests.get(url, timeout=5)
```

서버가 계속 응답하지 않을 때 무한정 기다리지 않도록 제한 시간을 정한다.

## JSON이 아닐 수도 있다

모든 응답이 JSON은 아니다.

```python
print(response.text)
```

은 응답 내용을 문자열로 본다.

```python
response.json()
```

은 응답이 JSON 형식이라고 예상하고 Python 자료형으로 바꾸려는 것이다.

JSON이 아닌 응답에서 `response.json()`을 호출하면 오류가 날 수 있다.

## API 키를 보내는 경우

API마다 방법이 다르지만 header를 사용하는 경우가 많다.

```python
headers = {
    "Authorization": "Bearer YOUR_API_KEY"
}

response = requests.get(url, headers=headers)
```

실제 키는 GitHub 같은 공개 저장소에 그대로 올리면 안 된다.

## API 호출을 확인하는 순서

처음에는 다음 순서로 보면 편하다.

```text
1. URL이 맞는가?
2. GET인지 POST인지 맞는가?
3. status_code가 무엇인가?
4. response.text에는 뭐가 들어오는가?
5. JSON이면 response.json()으로 바꾼다.
6. 필요한 key가 실제로 존재하는가?
```

## `KeyError`가 나는 경우

```python
data = response.json()
print(data["name"])
```

응답에 `name`이라는 key가 없으면 `KeyError`가 날 수 있다.

먼저 전체를 확인한다.

```python
print(data)
```

또는:

```python
print(data.get("name"))
```

## 초보용 안전한 예제 구조

```python
import requests

url = "https://example.com/api"

try:
    response = requests.get(url, timeout=5)

    print("상태 코드:", response.status_code)

    if 200 <= response.status_code < 300:
        print(response.text)
    else:
        print("API 요청 실패")

except requests.RequestException as e:
    print("네트워크 관련 오류:", e)
```

## 직접 연습

1. 공개 테스트 API에 GET 요청 보내기
2. `status_code` 출력하기
3. `text`와 `json()` 차이 확인하기
4. 일부러 잘못된 주소를 사용해 404 확인하기
5. `timeout` 넣어 보기
6. POST를 지원하는 테스트 API에 딕셔너리 보내 보기

API 코드는 처음부터 짧게 만들려고 하지 말고 **요청 → 상태 코드 → 원본 응답 → JSON 변환 → 필요한 값 꺼내기** 순서로 확인하는 것이 좋다.
