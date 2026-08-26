# 20. matplotlib로 첫 그래프 그리기

matplotlib는 Python에서 그래프를 그릴 때 많이 쓰는 라이브러리다. 처음에는 **숫자 목록을 그림으로 보여주는 도구**라고 생각하면 된다.

## 설치

터미널에서:

```text
pip install matplotlib
```

## 불러오기

```python
import matplotlib.pyplot as plt
```

보통 `plt`라는 짧은 이름으로 사용한다.

## 가장 간단한 선 그래프

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y)
plt.show()
```

`plt.plot()`은 그래프를 만들고 `plt.show()`는 화면에 보여준다.

## 막대그래프

```python
names = ["A", "B", "C"]
scores = [80, 95, 70]

plt.bar(names, scores)
plt.show()
```

## 제목과 축 이름

```python
plt.bar(names, scores)
plt.title("Score")
plt.xlabel("Student")
plt.ylabel("Score")
plt.show()
```

## 왜 그래프가 필요한가?

표로 보면 숫자를 하나씩 읽어야 하지만 그래프로 보면 어느 값이 큰지 작은지 빨리 볼 수 있다.

```text
표 = 정확한 숫자를 보기 좋음
그래프 = 전체 흐름과 차이를 보기 좋음
```

## 그래프가 안 뜰 때

Jupyter Notebook에서는 셀을 실행하면 바로 보이는 경우가 많다. 일반 `.py` 파일에서는 마지막에 `plt.show()`를 빼먹으면 창이 안 보일 수 있다.

## pandas와 같이 쓰기

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.DataFrame({
    "이름": ["철수", "영희", "민수"],
    "점수": [80, 95, 70]
})

plt.bar(df["이름"], df["점수"])
plt.show()
```

## 처음에는 이것만 기억

```text
plt.plot()  → 선 그래프
plt.bar()   → 막대그래프
plt.title() → 제목
plt.xlabel() → x축 이름
plt.ylabel() → y축 이름
plt.show()  → 화면에 보여주기
```

그래프 꾸미기는 나중 문제다. 처음에는 데이터가 제대로 들어갔는지와 축이 무엇을 뜻하는지를 이해하는 것이 먼저다.
