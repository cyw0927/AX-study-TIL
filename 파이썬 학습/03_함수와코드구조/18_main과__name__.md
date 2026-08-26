# `main()`과 `if __name__ == "__main__"` 아주 쉽게 이해하기

초보자가 처음 보면 가장 이상하게 생긴 코드 중 하나가 이것이다.

```python
if __name__ == "__main__":
    main()
```

처음에는 통째로 외우기 쉽지만, 뜻을 알면 그렇게 어렵지 않다.

## 먼저 `main()`은 특별한 문법이 아니다

`main`이라는 이름의 함수를 직접 만든 것뿐이다.

```python
def main():
    print("프로그램 시작")
```

이 상태에서는 함수만 만들어졌고 아직 실행되지 않는다.

실행하려면:

```python
main()
```

이라고 호출해야 한다.

## 왜 main에 코드를 넣나?

아주 짧은 프로그램은 그냥 위에서 아래로 적어도 된다.

```python
name = input("이름: ")
print(name)
```

하지만 코드가 길어지면 프로그램의 중심 흐름을 함수 안에 묶으면 읽기 편해진다.

```python
def main():
    name = input("이름: ")
    print(name)

main()
```

`main()`은 흔히 **프로그램의 시작 부분을 모아 놓은 함수 이름**으로 사용한다.

## `__name__`은 뭐지?

Python이 파일을 실행할 때 자동으로 만들어 주는 특별한 변수다.

파일을 직접 실행하면 `__name__`의 값은 다음과 같다.

```text
"__main__"
```

확인하려면:

```python
print(__name__)
```

파일을 직접 실행했을 때는 보통:

```text
__main__
```

이 나온다.

## 그래서 이 코드는 어떻게 읽나?

```python
if __name__ == "__main__":
    main()
```

초보자 말로 바꾸면:

> 이 Python 파일을 직접 실행한 거라면 `main()`을 실행해라.

정도로 생각하면 된다.

## 왜 그냥 main()을 쓰면 안 되나?

파일 하나만 쓸 때는 사실 이렇게 해도 실행된다.

```python
def main():
    print("안녕")

main()
```

문제는 다른 Python 파일에서 이 파일을 `import`할 때다.

예를 들어 `calculator.py`가 있다고 하자.

```python
def add(a, b):
    return a + b

print("calculator 실행됨")
```

다른 파일에서:

```python
import calculator
```

만 해도 `print()`가 실행될 수 있다.

그래서 직접 실행할 때만 돌아가야 하는 코드를 다음처럼 감싼다.

```python
def main():
    print("calculator 직접 실행")

if __name__ == "__main__":
    main()
```

## 과제 코드에서 보면

```python
def main():
    height, width = map(int, input().split())
    # 나머지 처리

if __name__ == "__main__":
    main()
```

이 코드는 다음처럼 읽으면 된다.

1. `main()`이라는 함수를 만든다.
2. 그 안에 프로그램 실행 순서를 넣는다.
3. 이 파일을 직접 실행했다면 `main()`을 호출한다.

## 당장 꼭 써야 하나?

아주 작은 연습 문제에서는 필수는 아니다.

```python
x = int(input())
print(x * 2)
```

이렇게 해도 된다.

하지만 코드가 길어지고 함수가 많아지면 `main()` 구조가 도움이 된다.

## 직접 확인해 보기

```python
def hello():
    print("hello 함수 실행")

print("현재 __name__:", __name__)

if __name__ == "__main__":
    hello()
```

먼저 직접 실행해서 결과를 보고, 나중에 `import`를 배울 때 다시 보면 차이가 더 잘 보인다.
