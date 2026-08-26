# pip 오류 기초

`pip install`을 했는데 설치가 안 되면 먼저 오류 마지막 줄부터 본다.

예:

```text
ERROR: Could not find a version that satisfies the requirement ...
```

또는:

```text
ModuleNotFoundError: No module named 'pandas'
```

## 가장 먼저 확인할 것 1: 가상환경

터미널 앞에 이런 표시가 있는지 본다.

```text
(.venv)
```

없다면 가상환경이 꺼져 있을 수 있다.

Windows PowerShell 예:

```powershell
.\.venv\Scripts\Activate.ps1
```

## 확인할 것 2: Python과 pip가 같은 환경인가?

```powershell
python --version
pip --version
```

둘 다 현재 프로젝트의 가상환경을 가리키는지 확인한다.

## 더 안전하게 설치하기

```powershell
python -m pip install pandas
```

이 방법은 지금 실행 중인 Python의 pip를 사용하라는 뜻이다.

## 패키지 이름 오타

```powershell
pip install panda
```

처럼 잘못 입력하면 엉뚱한 패키지를 설치하거나 오류가 날 수 있다.

보통은:

```powershell
pip install pandas
```

처럼 정확한 이름을 써야 한다.

## 설치했는데 import가 안 될 때

VS Code에서 선택된 Python 인터프리터와 터미널에서 설치한 환경이 다를 수 있다.

그래서 초보 단계에서는 다음 순서로 확인하면 좋다.

1. 가상환경 활성화
2. `python --version`
3. `python -m pip list`
4. 필요한 패키지가 있는지 확인
5. VS Code Python 인터프리터 확인

오류 메시지 전체를 무작정 읽기보다 **마지막 줄의 오류 이름 + 현재 가상환경**부터 확인한다.
