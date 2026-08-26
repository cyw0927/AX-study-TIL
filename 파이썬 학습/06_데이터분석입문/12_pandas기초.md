# 12. pandas 완전 기초

`pandas`는 표 형태의 데이터를 다룰 때 많이 사용하는 Python 패키지다.

엑셀처럼 행과 열이 있는 데이터를 코드로 정리하고 계산한다고 생각하면 쉽다.

## 설치

가상환경을 사용 중이라면 그 환경을 활성화한 뒤:

```powershell
python -m pip install pandas
```

## 불러오기

```python
import pandas as pd
```

`pandas`를 앞으로 `pd`라는 짧은 이름으로 부르겠다는 뜻이다.

## DataFrame

pandas에서 표 형태 데이터를 다루는 대표적인 구조다.

```python
import pandas as pd

data = {
    "name": ["철수", "영희", "민수"],
    "score": [80, 90, 70]
}

df = pd.DataFrame(data)
print(df)
```

대략 이런 표가 만들어진다.

```text
  name  score
0   철수     80
1   영희     90
2   민수     70
```

## 행과 열

`name`, `score`는 열(column)이다.

왼쪽의 0, 1, 2는 행 번호처럼 보이는 index다.

## 열 하나 보기

```python
print(df["score"])
```

## 여러 열 보기

```python
print(df[["name", "score"]])
```

대괄호가 두 겹인 이유는 여러 열 이름을 리스트로 전달하기 때문이다.

## 평균 구하기

```python
print(df["score"].mean())
```

## 합계 구하기

```python
print(df["score"].sum())
```

## 최댓값과 최솟값

```python
print(df["score"].max())
print(df["score"].min())
```

## 조건으로 골라내기

```python
high = df[df["score"] >= 80]
print(high)
```

점수가 80 이상인 행만 남긴다.

처음 보면 대괄호가 많아 어렵지만 순서를 쪼개서 보면 된다.

```python
condition = df["score"] >= 80
print(condition)
```

먼저 각 행이 조건에 맞는지 True/False가 나온다.

그 다음:

```python
high = df[condition]
```

처럼 조건에 맞는 행만 가져온다.

## CSV 읽기

```python
import pandas as pd

df = pd.read_csv("data.csv")
print(df)
```

CSV는 쉼표로 구분된 표 데이터 파일이다.

## 처음 몇 줄 보기

```python
print(df.head())
```

기본적으로 앞쪽 몇 행을 보여준다.

## 데이터 크기 보기

```python
print(df.shape)
```

예를 들어 `(100, 5)`라면 100행 5열이라는 뜻이다.

## 열 이름 보기

```python
print(df.columns)
```

## 자료형 보기

```python
print(df.dtypes)
```

## 값이 비어 있는지 확인

```python
print(df.isnull().sum())
```

각 열에 비어 있는 값이 몇 개인지 볼 때 자주 사용한다.

## 정렬

```python
sorted_df = df.sort_values("score", ascending=False)
print(sorted_df)
```

점수 높은 순으로 정렬한다.

## 그룹별 계산

예를 들어 데이터에 `team` 열이 있다면:

```python
print(df.groupby("team")["score"].mean())
```

팀별 평균 점수를 계산할 수 있다.

처음에는 이 코드가 길어 보여도 다음처럼 읽으면 된다.

```text
df
→ team 기준으로 묶고
→ score 열만 보고
→ 평균을 구한다
```

## 초보가 가장 먼저 익힐 pandas 흐름

```text
CSV 읽기
↓
head()로 눈으로 보기
↓
shape, columns, dtypes 확인
↓
필요한 열 선택
↓
조건으로 행 선택
↓
sum, mean, count 계산
↓
groupby로 묶어서 계산
```

## 직접 연습

```python
import pandas as pd

data = {
    "category": ["A", "A", "B", "B"],
    "sales": [100, 200, 300, 400]
}

df = pd.DataFrame(data)

print(df)
print(df["sales"].sum())
print(df["sales"].mean())
print(df.groupby("category")["sales"].sum())
```

각 출력이 왜 그렇게 나오는지 한 줄씩 확인한다.
