# 11. Jupyter Notebook 완전 기초

Jupyter Notebook은 코드를 작은 칸으로 나눠서 실행할 수 있는 학습 도구다. 파일 확장자는 보통 `.ipynb`다.

## `.py`와 `.ipynb` 차이

`.py`는 보통 위에서 아래로 한 번에 실행하는 Python 파일이다.

`.ipynb`는 코드를 여러 셀(cell)로 나눠서 필요한 부분만 실행할 수 있다.

예를 들어 첫 번째 셀:

```python
x = 10
```

두 번째 셀:

```python
print(x)
```

첫 번째 셀을 먼저 실행했다면 두 번째 셀에서 10이 나온다.

## 셀이란?

Notebook 안의 작은 칸이다.

주로 두 종류가 있다.

### 코드 셀

Python 코드를 실행하는 칸이다.

```python
print(1 + 2)
```

### Markdown 셀

설명 글을 적는 칸이다.

제목, 설명, 코드 해설 등을 적을 수 있다.

## 실행 순서가 중요하다

Notebook은 위에서 아래로만 실행해야 하는 것은 아니다. 그래서 실행 순서가 꼬일 수 있다.

예를 들어 두 번째 셀부터 실행하면:

```python
print(x)
```

`x`가 아직 만들어지지 않아 `NameError`가 날 수 있다.

## `Run All`

위에서 아래로 모든 셀을 순서대로 실행한다.

Notebook이 정상적으로 처음부터 끝까지 실행되는지 확인할 때 유용하다.

## Kernel이란?

Notebook 코드를 실제로 실행해 주는 Python 실행 환경이다.

VS Code에서 Notebook을 열었는데 실행이 안 된다면 어떤 Kernel이 선택되어 있는지 확인해야 한다.

가상환경 `.venv`를 사용한다면 Notebook Kernel도 그 `.venv`를 선택하는 것이 좋다.

## `ipykernel`

가상환경을 Notebook Kernel로 사용할 때 필요한 경우가 있다.

```powershell
python -m pip install ipykernel
```

## 실행 번호

셀 왼쪽에 `[1]`, `[2]` 같은 숫자가 표시될 수 있다. 이 숫자는 셀이 몇 번째로 실행되었는지 나타낸다.

화면 위쪽에 있다고 무조건 먼저 실행된 것은 아니다.

## Notebook에서 자주 생기는 혼란

### 이전에 만든 변수가 남아 있음

셀을 삭제했는데도 이전 실행에서 만든 변수가 메모리에 남아 있을 수 있다.

이럴 때 Kernel을 다시 시작한 뒤 `Run All`을 하면 현재 Notebook만으로 정상 실행되는지 확인할 수 있다.

### `input()` 때문에 멈춤

Notebook 셀 안에:

```python
name = input()
```

이 있으면 입력을 기다린다.

학습용 Notebook을 `Run All`로 한 번에 돌리고 싶다면 고정 예제 데이터를 사용하는 방법도 있다.

```python
name = "철수"
```

## Notebook이 학습에 좋은 이유

긴 프로그램을 한 번에 보지 않고 단계별로 확인할 수 있다.

```python
text = "255,0,0"
print(text)
```

다음 셀:

```python
parts = text.split(',')
print(parts)
```

다음 셀:

```python
r, g, b = map(int, parts)
print(r, g, b)
```

이렇게 중간 결과를 하나씩 볼 수 있다.

## 초보 사용법

1. Markdown 셀에서 이번에 확인할 내용을 적는다.
2. 코드 셀에는 작은 코드만 넣는다.
3. 실행 전에 결과를 한번 예상한다.
4. 실행 후 실제 결과를 본다.
5. 예상과 다르면 `print()`, `type()`, `len()`으로 확인한다.

## 직접 연습

첫 번째 셀:

```python
numbers = [10, 20, 30]
print(numbers)
```

두 번째 셀:

```python
print(len(numbers))
```

세 번째 셀:

```python
for number in numbers:
    print(number)
```

그다음 Kernel을 다시 시작하고 세 번째 셀만 실행했을 때 어떤 일이 생기는지도 확인해 본다.
