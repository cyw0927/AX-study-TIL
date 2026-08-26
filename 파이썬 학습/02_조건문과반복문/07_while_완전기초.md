# while문 완전 기초

`while`은 **조건이 참인 동안 계속 반복하는 문법**이다.

`for`가 '정해진 목록이나 횟수만큼 반복'하는 느낌이라면, `while`은 '이 조건이 계속 맞는 동안 반복'하는 느낌이다.

## 가장 작은 예제

```python
count = 1

while count <= 3:
    print(count)
    count += 1
```

결과:

```text
1
2
3
```

순서를 따라가면 이렇다.

```text
count = 1 → 1 <= 3 참 → 출력
count = 2 → 2 <= 3 참 → 출력
count = 3 → 3 <= 3 참 → 출력
count = 4 → 4 <= 3 거짓 → 반복 끝
```

## `count += 1`이 왜 중요한가?

다음 코드는 위험하다.

```python
count = 1

while count <= 3:
    print(count)
```

`count`가 계속 1이기 때문에 조건이 영원히 참이다.

그래서 1이 끝없이 출력된다. 이것을 **무한 반복**, **무한 루프**라고 한다.

## `while True`

조건 자리에 바로 `True`를 넣을 수도 있다.

```python
while True:
    text = input("종료하려면 q 입력: ")

    if text == "q":
        break
```

`True`는 항상 참이므로 그냥 두면 계속 반복된다.

그래서 안에서 `break`를 사용해 빠져나온다.

## `break`

반복문을 즉시 끝낸다.

```python
number = 1

while True:
    print(number)

    if number == 3:
        break

    number += 1
```

## `continue`

현재 반복의 남은 부분을 건너뛰고 다시 조건 검사로 돌아간다.

```python
number = 0

while number < 5:
    number += 1

    if number == 3:
        continue

    print(number)
```

3만 출력되지 않는다.

## for와 while 중 뭘 쓰지?

횟수가 뚜렷하면 보통 `for`가 읽기 쉽다.

```python
for i in range(5):
    print(i)
```

사용자가 특정 값을 입력할 때까지 반복하는 것처럼 종료 시점을 미리 모르면 `while`이 자연스럽다.

```python
while True:
    command = input("명령: ")
    if command == "종료":
        break
```

## 초보자가 자주 하는 실수

가장 흔한 것은 조건에 사용한 변수를 바꾸지 않는 것이다.

```python
x = 0
while x < 5:
    print(x)
```

이러면 계속 0이다.

고친 버전:

```python
x = 0
while x < 5:
    print(x)
    x += 1
```

## 직접 연습

비밀번호가 맞을 때까지 다시 입력받아 본다.

```python
password = "1234"

while True:
    user_input = input("비밀번호: ")

    if user_input == password:
        print("로그인 성공")
        break

    print("다시 입력하세요")
```

이 예제를 이해하면 `while`, `if`, `break`, `input()`이 어떻게 같이 움직이는지 한 번에 볼 수 있다.
