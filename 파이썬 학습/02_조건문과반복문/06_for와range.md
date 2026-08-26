# 06. for문과 range()

`for`는 같은 일을 여러 번 반복할 때 사용한다. 처음에는 `for`를 문법으로 외우기보다 **여러 개 중에서 하나씩 꺼내서 같은 일을 시킨다**고 생각하면 이해하기 쉽다.

## 리스트를 하나씩 꺼내기

```python
foods = ["짜장면", "짬뽕", "탕수육"]

for food in foods:
    print(food)
```

읽는 방법:

> foods 안에 있는 값을 하나씩 꺼내서 food라고 부르고 출력한다.

반복될 때마다 `food` 안의 값이 바뀐다.

```text
1번째 반복 → food = "짜장면"
2번째 반복 → food = "짬뽕"
3번째 반복 → food = "탕수육"
```

직접 눈으로 보고 싶으면 이렇게 해도 된다.

```python
foods = ["짜장면", "짬뽕", "탕수육"]

for food in foods:
    print("지금 food 안의 값:", food)
```

## `for 변수 in 여러개:` 모양 읽는 법

```python
for number in numbers:
```

이 문장을 한국말로 바꾸면:

```text
numbers 안에서 값을 하나씩 꺼낸다.
꺼낸 값을 잠깐 number라고 부른다.
아래 들여쓰기된 코드를 실행한다.
```

`number`라는 이름은 마음대로 바꿀 수 있다.

```python
for x in numbers:
    print(x)
```

다만 알아보기 쉬운 이름을 쓰는 게 좋다.

## 문자열도 반복할 수 있다

```python
for letter in "ABC":
    print(letter)
```

결과:

```text
A
B
C
```

문자열도 문자 여러 개가 모인 것이기 때문에 하나씩 꺼낼 수 있다.

## `range()`

숫자를 일정 범위만큼 만들어 준다.

```python
for i in range(5):
    print(i)
```

결과:

```text
0
1
2
3
4
```

`range(5)`는 0부터 4까지다. 5는 포함하지 않는다.

이게 헷갈리면 직접 리스트로 바꿔서 확인해 볼 수 있다.

```python
print(list(range(5)))
```

결과:

```text
[0, 1, 2, 3, 4]
```

## 시작 숫자 지정

```python
for i in range(1, 6):
    print(i)
```

결과는 1부터 5까지다.

```text
range(시작, 끝)
```

에서 끝 숫자는 포함하지 않는다.

## 증가 폭 지정

```python
for i in range(0, 10, 2):
    print(i)
```

결과:

```text
0
2
4
6
8
```

세 번째 숫자는 얼마씩 움직일지 정한다.

```text
range(0, 10, 2)
      시작 끝 2씩 증가
```

거꾸로 갈 수도 있다.

```python
for i in range(5, 0, -1):
    print(i)
```

결과:

```text
5
4
3
2
1
```

## 반복 횟수만 필요할 때

반복 횟수만 중요하고 숫자 자체는 사용하지 않을 때 `_`를 자주 쓴다.

```python
for _ in range(3):
    print("안녕")
```

`_`도 사실 변수 이름이지만 "이 값은 딱히 안 쓸 거야"라는 뜻으로 많이 사용한다.

## 누적하기

반복문에서 아주 자주 나오는 형태다.

```python
numbers = [10, 20, 30]
total = 0

for number in numbers:
    total = total + number
    print("number:", number)
    print("total:", total)
```

`total`은 이렇게 바뀐다.

```text
처음: 0
10을 더함: 10
20을 더함: 30
30을 더함: 60
```

`total = total + number`는 다음처럼 줄여 쓸 수 있다.

```python
total += number
```

## 리스트에 결과 모으기

반복하면서 계산한 값을 새 리스트에 저장하는 것도 자주 한다.

```python
numbers = [1, 2, 3]
results = []

for number in numbers:
    doubled = number * 2
    results.append(doubled)

print(results)
```

결과:

```text
[2, 4, 6]
```

과정을 쪼개면:

```text
1을 꺼냄 → 2로 계산 → results에 추가
2를 꺼냄 → 4로 계산 → results에 추가
3을 꺼냄 → 6으로 계산 → results에 추가
```

## 중첩 for문

for문 안에 for문이 들어갈 수 있다.

```python
board = [
    [1, 2, 3],
    [4, 5, 6]
]

for row in board:
    for number in row:
        print(number)
```

바깥 반복문은 행을 하나씩 꺼내고, 안쪽 반복문은 그 행 안의 값을 하나씩 꺼낸다.

처음 반복을 자세히 보면:

```text
바깥 for: row = [1, 2, 3]
    안쪽 for: number = 1
    안쪽 for: number = 2
    안쪽 for: number = 3

바깥 for: row = [4, 5, 6]
    안쪽 for: number = 4
    안쪽 for: number = 5
    안쪽 for: number = 6
```

## 왜 이미지 문제에서 for문을 두 번 쓰나?

이미지는 보통 행과 열로 되어 있기 때문이다.

```text
첫 번째 행: 픽셀 픽셀 픽셀
두 번째 행: 픽셀 픽셀 픽셀
세 번째 행: 픽셀 픽셀 픽셀
```

그래서 먼저 행을 반복하고 그 안에서 픽셀을 반복한다.

```python
image = [
    [10, 20, 30],
    [40, 50, 60]
]

for row in image:
    print("현재 행:", row)

    for pixel in row:
        print("현재 픽셀:", pixel)
```

이런 식으로 중간값을 출력하면 중첩 반복문의 움직임이 눈에 보인다.

## `break`

반복문을 바로 끝낸다.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

0부터 4까지만 출력된다.

`i == 5`가 되는 순간 반복 자체를 종료한다.

## `continue`

현재 반복만 건너뛰고 다음 반복으로 넘어간다.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

2만 빠진다.

```text
0 → 출력
1 → 출력
2 → continue라서 출력 건너뜀
3 → 출력
4 → 출력
```

## `enumerate()`

값과 위치 번호를 같이 받고 싶을 때 편하다.

```python
foods = ["짜장면", "짬뽕", "탕수육"]

for index, food in enumerate(foods):
    print(index, food)
```

결과:

```text
0 짜장면
1 짬뽕
2 탕수육
```

위치 번호를 1부터 시작하고 싶으면:

```python
for index, food in enumerate(foods, start=1):
    print(index, food)
```

## `while`과 차이

`for`는 보통 반복할 대상이나 횟수가 정해져 있을 때 편하다.

```python
for i in range(5):
    print(i)
```

`while`은 어떤 조건이 참인 동안 계속 반복한다.

```python
count = 0

while count < 5:
    print(count)
    count += 1
```

둘 다 0부터 4까지 출력하지만 생각하는 방식이 다르다.

```text
for   = 이 여러 개를 하나씩 처리해
while = 이 조건이 참인 동안 계속해
```

## 자주 하는 실수 1: 들여쓰기 위치

```python
total = 0
for number in [1, 2, 3]:
    total += number
    print(total)
```

이 코드는 중간 합계를 매번 출력한다.

최종 합계만 출력하려면:

```python
total = 0
for number in [1, 2, 3]:
    total += number

print(total)
```

들여쓰기 한 단계 차이가 결과를 바꾼다.

## 자주 하는 실수 2: `range(5)`에 5도 들어간다고 생각함

```python
print(list(range(5)))
```

을 직접 실행해서 확인한다.

## 자주 하는 실수 3: 리스트를 반복하면서 리스트를 함부로 바꿈

처음에는 반복 중인 리스트 자체를 삭제하거나 크게 변경하는 코드는 피하는 게 좋다.

```python
numbers = [1, 2, 3]

for number in numbers:
    print(number)
```

이 기본 형태를 먼저 익힌 다음 리스트 변경을 배우는 편이 안전하다.

## 직접 연습 1

```python
numbers = [10, 20, 30, 40]
total = 0

for number in numbers:
    total += number
    print("현재 숫자:", number)
    print("현재 합계:", total)

print("최종 합계:", total)
```

각 반복에서 `number`와 `total`이 어떻게 바뀌는지 눈으로 확인한다.

## 직접 연습 2

1부터 10까지 숫자 중 짝수만 출력해 본다.

```python
for number in range(1, 11):
    if number % 2 == 0:
        print(number)
```

## 직접 연습 3

다음 2차원 리스트의 모든 숫자를 출력해 본다.

```python
numbers = [
    [1, 2],
    [3, 4],
    [5, 6]
]
```

정답을 바로 보지 말고 바깥 for문이 무엇을 꺼내야 하는지부터 생각한다.
