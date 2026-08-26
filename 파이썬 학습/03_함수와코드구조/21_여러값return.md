# 여러 값을 return 하기

함수는 값 하나만 돌려주는 것처럼 보이지만 여러 값을 한꺼번에 돌려줄 수도 있다.

```python
def calc(a, b):
    return a + b, a - b

result = calc(10, 3)
print(result)
```

결과:

```text
(13, 7)
```

여러 값을 return하면 실제로는 튜플 형태로 묶여서 돌아온다.

## 바로 나눠 받기

```python
def calc(a, b):
    return a + b, a - b

plus, minus = calc(10, 3)

print(plus)
print(minus)
```

결과:

```text
13
7
```

이걸 언패킹이라고 부른다.

너무 어렵게 생각하지 말고 이렇게 보면 된다.

```text
함수 결과: (13, 7)
plus = 13
minus = 7
```

## 자주 보는 예

```python
def get_name_age():
    return "철수", 20

name, age = get_name_age()
print(name)
print(age)
```

`return` 뒤에 값이 여러 개 있다고 놀랄 필요 없다. 여러 값을 묶어서 보내고, 받을 때 다시 나눠 받을 수 있다.
