# 06. for문과 range()

`for`는 같은 일을 여러 번 반복할 때 사용한다.

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

## 시작 숫자 지정

```python
for i in range(1, 6):
    print(i)
```

결과는 1부터 5까지다.

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

## 반복 횟수만 필요할 때

반복 횟수만 중요하고 숫자 자체는 사용하지 않을 때 `_`를 자주 쓴다.

```python
for _ in range(3):
    print("안녕")
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

## 왜 이미지 문제에서 for문을 두 번 쓰나?

이미지는 보통 행과 열로 되어 있기 때문이다.

```text
첫 번째 행: 픽셀 픽셀 픽셀
두 번째 행: 픽셀 픽셀 픽셀
세 번째 행: 픽셀 픽셀 픽셀
```

그래서 먼저 행을 반복하고 그 안에서 픽셀을 반복한다.

## `break`

반복문을 바로 끝낸다.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

0부터 4까지만 출력된다.

## `continue`

현재 반복만 건너뛰고 다음 반복으로 넘어간다.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

2만 빠진다.

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

## 자주 하는 실수

### 반복문 밖에 있어야 할 코드를 안에 넣는 경우

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

## 직접 연습

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
