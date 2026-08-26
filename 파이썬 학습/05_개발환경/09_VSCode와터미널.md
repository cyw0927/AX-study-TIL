# 09. VS Code와 터미널 완전 기초

Python 코드를 배우다 보면 VS Code, 터미널, PowerShell 같은 말을 자주 보게 된다. 처음에는 각각 뭐가 다른지 헷갈리기 쉽다.

## VS Code

코드를 작성하고 파일을 관리하는 프로그램이다.

메모장에서도 Python 코드를 쓸 수는 있지만 VS Code는 코드 색깔, 자동완성, 오류 표시, 터미널 같은 기능을 제공해서 훨씬 편하다.

## 터미널

글자로 컴퓨터에게 명령을 내리는 창이다.

Windows에서는 PowerShell을 자주 사용한다.

예:

```powershell
python hello.py
```

이 명령은 `hello.py`라는 Python 파일을 실행하라는 뜻이다.

## 현재 폴더가 왜 중요한가?

터미널은 항상 어떤 폴더 안에 들어가 있다.

```powershell
Get-Location
```

현재 위치를 확인할 수 있다.

예를 들어 현재 폴더에 `problem02.py`가 없다면:

```powershell
python problem02.py
```

를 실행해도 파일을 찾지 못할 수 있다.

## `cd`

폴더를 이동하는 명령이다.

```powershell
cd C:\dev\project
```

중요: `cd`는 Git 명령이 아니다.

```powershell
git cd C:\dev\project
```

처럼 쓰지 않는다.

## `dir`

현재 폴더의 파일 목록을 본다.

```powershell
dir
```

실행하려는 `.py` 파일이 실제로 있는지 확인할 때 유용하다.

## Python 파일 실행하기

```powershell
python test.py
```

Python이 설치되어 있고 파일 경로가 맞으면 실행된다.

## `>>>`가 보이면?

터미널에서 `python`만 입력하면 Python 대화형 모드로 들어갈 수 있다.

```text
>>>
```

여기서는 PowerShell 명령이 아니라 Python 코드를 입력해야 한다.

빠져나오려면:

```python
exit()
```

을 입력한다.

## 터미널과 Python 코드를 섞지 않기

PowerShell에서 쓰는 것:

```powershell
cd C:\dev
python test.py
git status
```

Python 코드 안에서 쓰는 것:

```python
print("hello")
name = input()
```

둘은 다른 종류의 명령이다.

## VS Code에서 Python 선택

VS Code는 어떤 Python을 사용할지 선택해야 할 때가 있다.

Command Palette 또는 아래쪽 상태 표시에서 Python Interpreter를 선택할 수 있다.

가상환경 `.venv`를 만들었다면 보통 그 안의 Python을 선택한다.

## 파일 저장도 중요하다

코드를 수정하고 저장하지 않은 상태에서 터미널로 실행하면 이전 내용이 실행될 수 있다.

실행 전에 `Ctrl + S`로 저장하는 습관을 들이면 좋다.

## 초보 확인 순서

프로그램이 실행되지 않을 때 다음 순서로 본다.

1. 파일을 저장했는가?
2. 터미널 현재 폴더가 맞는가?
3. `dir`에 파일이 보이는가?
4. `python 파일이름.py`를 정확히 입력했는가?
5. 실행 후 `input()`을 기다리고 있는 것은 아닌가?
6. 오류 메시지 마지막 줄은 무엇인가?

## 직접 연습

터미널에서:

```powershell
Get-Location
dir
python --version
```

을 각각 실행해 본다.

그 다음 간단한 파일을 만든다.

```python
print("실행 성공")
```

파일 이름을 `hello.py`로 저장한 후:

```powershell
python hello.py
```

로 실행한다.
