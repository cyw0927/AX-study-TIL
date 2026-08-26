# 10. 가상환경과 pip

처음 Python을 배우면 `.venv`, `pip`, 패키지 같은 말이 갑자기 나온다. 처음에는 전부 외우지 말고 **프로젝트마다 필요한 도구를 따로 관리하는 방법**이라고 이해하면 된다.

## 패키지란?

다른 사람이 미리 만들어 둔 Python 기능 묶음이다.

예를 들어 데이터 분석을 할 때 많이 쓰는 `pandas`, 그래프를 그릴 때 쓰는 `matplotlib` 같은 것이 있다.

Python 기본 기능만으로도 많은 일을 할 수 있지만, 패키지를 설치하면 이미 만들어진 기능을 가져다 쓸 수 있다.

## `pip`란?

Python 패키지를 설치하는 도구다.

```powershell
pip install pandas
```

또는 더 확실하게:

```powershell
python -m pip install pandas
```

이라고 쓸 수 있다.

## 가상환경이란?

프로젝트 전용 Python 공간이라고 생각하면 쉽다.

예를 들어 프로젝트 A는 어떤 패키지의 옛날 버전을 쓰고, 프로젝트 B는 최신 버전을 써야 할 수 있다. 모두 한곳에 설치하면 충돌할 수 있다.

가상환경을 만들면 프로젝트마다 패키지를 따로 관리할 수 있다.

## `.venv` 만들기

프로젝트 폴더에서:

```powershell
python -m venv .venv
```

실행하면 `.venv`라는 폴더가 생긴다.

`.venv`라는 이름은 관습적으로 많이 쓰는 이름이고 꼭 이 이름만 가능한 것은 아니다.

## Windows PowerShell에서 활성화

```powershell
.\.venv\Scripts\Activate.ps1
```

활성화되면 터미널 앞에 다음처럼 보일 수 있다.

```text
(.venv) PS C:\dev\project>
```

이제 이 터미널에서 설치하는 패키지는 보통 현재 가상환경에 설치된다.

## 가상환경 종료

```powershell
deactivate
```

## 현재 Python 확인

```powershell
python --version
```

Python 코드에서 실행 경로도 확인할 수 있다.

```python
import sys
print(sys.executable)
```

가상환경을 제대로 사용 중이라면 경로에 `.venv`가 포함될 수 있다.

## 설치된 패키지 보기

```powershell
pip list
```

또는:

```powershell
python -m pip list
```

## 패키지 설치

```powershell
python -m pip install pandas
```

여러 개를 설치할 수도 있다.

```powershell
python -m pip install pandas matplotlib
```

## 패키지 제거

```powershell
python -m pip uninstall pandas
```

## `requirements.txt`

프로젝트가 어떤 패키지를 사용하는지 목록으로 적어 두는 파일이다.

예:

```text
Flask
pandas
matplotlib
```

한꺼번에 설치할 때:

```powershell
python -m pip install -r requirements.txt
```

## 자주 하는 실수

### 패키지를 설치했는데 import가 안 됨

터미널에서 설치한 Python과 VS Code에서 선택한 Python이 서로 다를 수 있다.

이때 확인할 것:

```powershell
python --version
python -m pip list
```

그리고 VS Code의 Python Interpreter도 같은 가상환경인지 확인한다.

### `.venv`를 GitHub에 올려야 하나?

보통은 올리지 않는다. `.venv`는 컴퓨터마다 다시 만들 수 있고 파일 수도 많다.

그래서 `.gitignore`에 다음을 넣는 경우가 많다.

```text
.venv/
```

## 초보가 기억할 최소 내용

```text
python -m venv .venv                → 가상환경 만들기
.\.venv\Scripts\Activate.ps1       → Windows에서 활성화
python -m pip install 패키지이름    → 패키지 설치
deactivate                          → 가상환경 나오기
```

처음에는 이 네 개만 알아도 충분하다.
