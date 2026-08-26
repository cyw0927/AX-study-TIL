# requirements.txt가 뭔가요?

Python 프로젝트에는 외부 라이브러리를 여러 개 설치해서 쓰는 경우가 많다.

예를 들어 Flask 프로젝트라면:

```text
Flask
requests
pandas
```

이런 패키지가 필요할 수 있다.

`requirements.txt`는 **이 프로젝트에 필요한 패키지 목록을 적어 놓는 파일**이다.

예:

```text
Flask==3.1.2
requests==2.32.5
pandas==2.3.2
```

`==` 뒤 숫자는 버전이다.

## 설치 방법

터미널에서:

```powershell
pip install -r requirements.txt
```

여기서 `-r`은 requirements 파일을 읽어서 설치하라는 뜻이라고 생각하면 된다.

## 현재 설치된 패키지 확인

```powershell
pip list
```

## 현재 환경을 파일로 저장

```powershell
pip freeze > requirements.txt
```

하지만 초보 단계에서는 무조건 `pip freeze`를 쓰기보다, 실제 프로젝트에서 필요한 패키지만 직접 적는 방법도 알아두는 게 좋다.

## 왜 필요한가?

내 컴퓨터에서는 Flask가 설치돼 있어서 잘 실행되는데 다른 컴퓨터에는 Flask가 없으면 실행이 안 될 수 있다.

그럴 때 `requirements.txt`가 있으면 필요한 패키지를 한꺼번에 설치할 수 있다.

한 줄 요약:

```text
requirements.txt = 이 프로젝트가 필요로 하는 Python 패키지 목록
```
