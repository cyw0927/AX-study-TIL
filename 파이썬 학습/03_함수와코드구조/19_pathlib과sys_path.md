# 19. pathlib과 sys.path 쉽게 이해하기

프로젝트를 하다 보면 코드 자체보다 **파일 경로와 import 문제** 때문에 막히는 일이 많다.

`pathlib`과 `sys.path`는 이럴 때 자주 등장한다.

---

## 1. pathlib은 경로를 다루는 도구

```python
from pathlib import Path
```

이 코드는 파이썬에서 파일과 폴더 경로를 편하게 다루기 위해 `Path`를 가져오는 것이다.

예:

```python
current = Path.cwd()
print(current)
```

현재 작업 중인 폴더 경로를 보여 준다.

---

## 2. `/`로 경로를 이어 붙일 수 있다

```python
project_root = Path.cwd()
data_dir = project_root / "data" / "raw"
```

문자열을 직접 더하는 것보다 읽기 쉽다.

```text
project_root
↓
data
↓
raw
```

즉 `data/raw` 폴더를 가리킨다.

---

## 3. exists()

```python
print(data_dir.exists())
```

해당 파일이나 폴더가 실제로 존재하는지 확인한다.

결과는 `True` 또는 `False`다.

경로 문제가 생겼을 때 매우 자주 쓴다.

---

## 4. parent

```python
parent_dir = Path.cwd().parent
```

현재 폴더의 상위 폴더를 뜻한다.

예를 들어 현재 위치가:

```text
C:/dev/project/notebooks
```

이면 `.parent`는:

```text
C:/dev/project
```

가 된다.

---

## 5. sys.path는 import할 곳 목록

```python
import sys
print(sys.path)
```

파이썬이 `import`할 때 파일이나 모듈을 찾는 경로 목록이다.

쉽게 말하면:

```text
"파이썬아, 모듈 찾을 때 여기들을 뒤져봐"
```

라는 목록이다.

---

## 6. 왜 ModuleNotFoundError가 생기는가

예를 들어:

```python
from src.paths import DATA_DIR
```

라고 했는데 파이썬이 `src` 폴더를 찾지 못하면:

```text
ModuleNotFoundError
```

가 발생할 수 있다.

이때 확인할 것:

```python
from pathlib import Path
import sys

print(Path.cwd())
print(sys.path)
```

현재 실행 위치와 import 검색 경로를 확인한다.

---

## 7. 프로젝트 루트를 sys.path에 추가하는 경우

Notebook이 하위 폴더에 있을 때 프로젝트 루트를 추가해서 해결하기도 한다.

```python
from pathlib import Path
import sys

project_root = Path.cwd().parent

if str(project_root) not in sys.path:
    sys.path.append(str(project_root))
```

뜻은:

```text
프로젝트 최상위 폴더를 구한다
↓
sys.path에 아직 없으면
↓
import 검색 경로에 추가한다
```

---

## 8. 무조건 append부터 하면 안 된다

경로 문제를 만나면 무조건 `sys.path.append()`부터 복붙하기보다 먼저 확인한다.

```python
print(Path.cwd())
print(project_root)
print(project_root.exists())
print(sys.path)
```

현재 내가 어디에서 실행 중인지부터 이해해야 한다.

---

## 9. Notebook에서 특히 자주 헷갈리는 이유

VS Code에서 프로젝트 폴더를 열었더라도 Jupyter Notebook의 현재 작업 위치가 예상과 다를 수 있다.

따라서 파일을 못 찾거나 import가 안 될 때는 제일 먼저:

```python
from pathlib import Path
print(Path.cwd())
```

를 실행한다.

---

## 핵심 정리

```text
Path
-> 파일/폴더 경로를 편하게 다룸

Path.cwd()
-> 현재 작업 위치

.parent
-> 한 단계 위 폴더

.exists()
-> 실제 존재 여부 확인

sys.path
-> Python이 import할 때 찾아보는 경로 목록
```

경로 오류가 나면 코드를 마구 바꾸기보다 **현재 위치부터 확인한다.**
