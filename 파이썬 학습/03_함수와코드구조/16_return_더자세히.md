# return 더 자세히

`return`은 함수가 만든 결과를 **함수 밖으로 돌려주는 것**이다.

`print()`와 `return`은 완전히 같은 것이 아니다.

## `print()`만 있는 함수

```python
def add(a, b):
    print(a + b)

result = add(3, 5)
print("result:", result)
```

함수 안에서는 `8`이 출력되지만 `result`에는 `None`이 들어간다.

왜냐하면 이 함수는 값을 출력만 했고 돌려주지는 않았기 때문이다.

## `return`이 있는 함수

```python
def add(a, b):
    return a + b

result = add(3, 5)
print(result)
```

이번에는 `result`에 8이 들어간다.

## 쉽게 생각하기

```text
print()  = 화면에 보여주기
return   = 결과를 함수 밖으로 넘겨주기
```

## return을 받자마자 다른 계산도 가능

```python
def add(a, b):
    return a + b

answer = add(3, 5) * 10
print(answer)
```

결과는 `80`이다.

## return을 만나면 함수는 끝난다

```python
def test():
    print("첫 번째")
    return 10
    print("두 번째")
```

`return` 아래의 `print("두 번째")`는 실행되지 않는다.

## 조건문과 return

```python
def check_age(age):
    if age >= 19:
        return "성인"
    else:
        return "미성년자"
```

```python
result = check_age(20)
print(result)
```

## 여러 값을 돌려주기

```python
def calculate(a, b):
    total = a + b
    difference = a - b
    return total, difference

x, y = calculate(10, 3)
print(x)
print(y)
```

Python은 여러 값을 한 번에 돌려주는 것처럼 쓸 수도 있다.

초보 단계에서는 먼저 **return 하나**부터 익힌 뒤 이런 문법으로 넘어가면 된다.

## 왜 return이 필요한가?

함수를 재사용하기 좋아진다.

```python
def brightness(r, g, b):
    return (r + g + b) // 3

b1 = brightness(255, 0, 0)
b2 = brightness(0, 255, 0)
print(b1, b2)
```

함수 안에서 무조건 출력해 버리는 대신 결과를 받아서 다음 계산에 사용할 수 있다.

## 자주 하는 실수

### return을 쓰고도 결과를 저장하지 않음

```python
def add(a, b):
    return a + b

add(3, 5)
```

계산은 됐지만 화면에는 아무것도 안 나온다.

확인하려면:

```python
print(add(3, 5))
```

또는:

```python
result = add(3, 5)
print(result)
```

## 직접 연습

```python
def square(number):
    return number * number

result = square(5)
print(result)
```

그다음 `return`을 `print()`로 바꾸고 `result`가 어떻게 달라지는지 비교해 본다.
