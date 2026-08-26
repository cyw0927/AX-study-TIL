# JSON 읽기

JSON은 API를 공부하면 정말 자주 만나는 데이터 모양이다.

겉보기에는 Python 딕셔너리와 비슷하다.

```json
{
  "name": "철수",
  "age": 20,
  "skills": ["python", "sql"]
}
```

## Python으로 바꾸면

보통 이런 느낌이다.

```python
data = {
    "name": "철수",
    "age": 20,
    "skills": ["python", "sql"]
}
```

## 값 꺼내기

```python
print(data["name"])
print(data["age"])
```

리스트 안의 값도 꺼낼 수 있다.

```python
print(data["skills"][0])
```

결과는 `python`이다.

## 중첩된 JSON

API 응답은 여러 겹으로 들어오는 경우가 많다.

```python
data = {
    "user": {
        "name": "철수",
        "score": 90
    }
}

print(data["user"]["name"])
```

처음에는 한 번에 읽으려고 하지 말고 한 단계씩 꺼내 보면 된다.

```python
user = data["user"]
print(user)
print(type(user))
print(user["name"])
```

이 방식이 초보에게 훨씬 보기 쉽다.

## 리스트가 섞인 경우

```python
data = {
    "students": [
        {"name": "철수", "score": 90},
        {"name": "영희", "score": 85}
    ]
}
```

첫 번째 학생:

```python
first = data["students"][0]
print(first)
print(first["name"])
```

전체 학생 반복:

```python
for student in data["students"]:
    print(student["name"], student["score"])
```

## `.get()` 사용하기

딕셔너리에 키가 없을 때 바로 오류가 나는 것을 피하고 싶다면:

```python
print(data.get("name"))
```

키가 없으면 기본적으로 `None`이 나온다.

기본값도 정할 수 있다.

```python
print(data.get("address", "주소 없음"))
```

## JSON 문자열과 Python 딕셔너리는 완전히 같은 건 아니다

JSON은 데이터를 주고받을 때 사용하는 텍스트 형식이고, Python에서는 그것을 딕셔너리와 리스트로 바꿔서 다루는 경우가 많다.

`requests`에서는:

```python
response = requests.get("API 주소")
data = response.json()
```

처럼 받아온 JSON을 Python 자료형으로 바꿔준다.

## 처음 보는 API 응답을 읽는 순서

```python
print(type(data))
print(data)
```

그다음:

1. 제일 바깥이 딕셔너리인지 리스트인지 확인한다.
2. 딕셔너리라면 키 이름을 본다.
3. 리스트라면 첫 번째 값부터 확인한다.
4. 다시 `type()`을 찍는다.
5. 한 단계씩 필요한 값까지 내려간다.

JSON은 한 번에 전체 구조를 외우는 것보다 **껍질을 한 겹씩 벗긴다**고 생각하면 쉽다.
