# 19. pandas 한 단계 더

기초에서 `DataFrame`이 표라는 것까지 봤다면 이제는 실제로 표를 조금씩 골라 보고 계산해 본다.

```python
import pandas as pd

data = {
    "이름": ["철수", "영희", "민수"],
    "점수": [80, 95, 70],
    "지역": ["서울", "부산", "서울"]
}

df = pd.DataFrame(data)
print(df)
```

## 열 하나 보기

```python
print(df["점수"])
```

표 전체가 아니라 점수 열만 본다.

## 열 여러 개 보기

```python
print(df[["이름", "점수"]])
```

대괄호가 두 겹처럼 보여서 처음에 헷갈리기 쉽다.

```text
df["점수"]          → 열 하나
df[["이름", "점수"]] → 열 여러 개
```

## 조건으로 행 고르기

```python
print(df[df["점수"] >= 80])
```

점수가 80 이상인 행만 남는다.

과정을 쪼개 보면:

```python
condition = df["점수"] >= 80
print(condition)
print(df[condition])
```

처음에는 이렇게 중간값을 따로 출력해 보는 게 이해하기 쉽다.

## 정렬

```python
print(df.sort_values("점수"))
```

큰 점수부터 보고 싶으면:

```python
print(df.sort_values("점수", ascending=False))
```

`ascending=False`는 오름차순이 아니게, 즉 큰 값부터 정렬하라는 뜻이다.

## 평균

```python
print(df["점수"].mean())
```

## 지역별 평균

```python
print(df.groupby("지역")["점수"].mean())
```

이 코드는 처음 보면 길다. 세 부분으로 나누면 된다.

```text
df.groupby("지역") → 지역이 같은 것끼리 묶기
["점수"]           → 점수 열 보기
.mean()             → 평균 계산
```

## 새 열 만들기

```python
df["합격"] = df["점수"] >= 80
print(df)
```

`합격`이라는 새 열이 생기고 `True`, `False`가 들어간다.

## CSV 읽기

```python
df = pd.read_csv("data.csv")
```

파일 경로가 틀리면 `FileNotFoundError`가 날 수 있다.

## 데이터 처음 확인할 때 자주 쓰는 것

```python
print(df.head())
print(df.shape)
print(df.columns)
print(df.info())
```

처음 보는 데이터는 바로 분석하지 말고 먼저 모양과 열 이름부터 확인한다.

## 초보가 많이 하는 실수

열 이름의 띄어쓰기나 철자가 실제 파일과 다르면 오류가 난다.

```python
print(df.columns)
```

을 먼저 실행해서 실제 열 이름을 확인하는 습관이 좋다.

## 직접 연습

학생 5명의 이름, 점수, 지역을 DataFrame으로 만든 다음 아래를 해 본다.

1. 점수만 출력하기
2. 80점 이상만 고르기
3. 점수 높은 순으로 정렬하기
4. 전체 평균 구하기
5. 지역별 평균 구하기

한 줄짜리 코드를 외우는 것보다 중간 결과를 `print()`로 확인하면서 진행한다.
