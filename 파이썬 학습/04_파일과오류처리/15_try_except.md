# 15. try / except 완전 기초

프로그램을 실행하다가 오류가 날 수 있다는 것을 미리 알고 있다면, 오류가 나도 프로그램이 바로 끝나지 않도록 처리할 수 있다.

이때 사용하는 것이 `try`와 `except`다.

## 가장 기본적인 모양

```python
try:
    number = int(input("숫자 입력: "))
    print(number)
except:
    print("숫자로 바꿀 수 없습니다")
```

숫자를 입력하면 정상 실행된다.

`abc` 같은 글자를 입력해도 프로그램이 갑자기 끝나는 대신 우리가 정한 문장을 보여줄 수 있다.

## 어떻게 읽으면 되나?

```text
try
→ 일단 이 코드를 실행해 본다.

except
→ 실행하다 오류가 나면 이쪽 코드를 실행한다.
```

## 오류 종류를 지정하는 것이 좋다

모든 오류를 한꺼번에 잡는 것보다 어떤 오류를 예상하는지 적는 것이 좋다.

```python
try:
    number = int("abc")
except ValueError:
    print("정수로 바꿀 수 없는 값입니다")
```

## 여러 오류 처리

```python
try:
    numbers = [10, 20, 30]
    index = int(input("위치 입력: "))
    print(numbers[index])
except ValueError:
    print("숫자를 입력해야 합니다")
except IndexError:
    print("없는 위치입니다")
```

## `else`

오류가 없었을 때 실행할 코드를 따로 적을 수 있다.

```python
try:
    number = int(input())
except ValueError:
    print("잘못된 입력")
else:
    print("입력 성공:", number)
```

## `finally`

오류가 나든 안 나든 마지막에 실행된다.

```python
try:
    print("실행")
except:
    print("오류")
finally:
    print("마지막에 실행")
```

처음에는 `finally`까지 자주 쓸 필요는 없지만 이런 문법이 있다는 정도는 알아두면 된다.

## 파일 열기와 같이 쓰기

```python
try:
    with open("memo.txt", "r", encoding="utf-8") as file:
        print(file.read())
except FileNotFoundError:
    print("파일을 찾을 수 없습니다")
```

## try/except를 너무 많이 쓰면 안 되는 이유

오류가 왜 났는지 모르는데 전부 감춰버리면 디버깅이 더 어려워질 수 있다.

```python
try:
    # 아주 긴 코드
    ...
except:
    print("오류")
```

이렇게 쓰면 실제 원인을 알기 어렵다.

처음에는:

1. 어떤 오류가 날 수 있는지 확인하고
2. 오류 종류를 알고
3. 필요한 부분만 `try`로 감싸는 것이 좋다.

## 디버깅 단계와 사용자용 처리 단계는 다르다

공부 중에는 오류 메시지를 직접 보는 것도 중요하다.

무조건 `try/except`로 감추지 말고, 먼저 오류를 읽고 원인을 이해한다.

그 다음 사용자가 잘못된 값을 넣어도 프로그램이 친절하게 처리하도록 만들고 싶을 때 `try/except`를 사용한다.

## 직접 연습

```python
while True:
    try:
        age = int(input("나이 입력: "))
        break
    except ValueError:
        print("숫자로 입력해주세요")

print("입력한 나이:", age)
```

문자를 입력했을 때와 숫자를 입력했을 때 흐름이 어떻게 달라지는지 확인한다.
