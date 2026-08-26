# .gitignore 기초

`.gitignore`는 **Git이 추적하지 않았으면 하는 파일이나 폴더를 적어 놓는 파일**이다.

예를 들어 Python 프로젝트에서는 가상환경 폴더를 GitHub에 올릴 필요가 없는 경우가 많다.

```text
.venv/
```

또 환경변수 파일도 보통 올리지 않는다.

```text
.env
```

예시 `.gitignore`:

```text
.venv/
__pycache__/
.env
*.pyc
```

## 왜 필요한가?

프로젝트에 필요한 코드만 Git으로 관리하고, 자동으로 생기는 파일이나 개인 설정 파일은 제외하기 위해서다.

특히 `.env`에는 API 키나 비밀번호 같은 민감한 값이 들어갈 수 있으므로 GitHub에 올리지 않도록 주의해야 한다.

## 이미 Git이 추적 중이면?

중요한 점이 있다.

`.gitignore`에 적었다고 해서 이미 Git이 추적 중인 파일이 자동으로 사라지는 것은 아니다.

예를 들어 `.env`를 이미 commit했다면 별도 조치가 필요하다.

```powershell
git rm --cached .env
```

폴더라면:

```powershell
git rm -r --cached .venv
```

그다음 commit한다.

## 확인하기

```powershell
git status
```

무시하려는 파일이 더 이상 변경 목록에 나타나지 않는지 확인한다.

한 줄 요약:

```text
.gitignore = Git에게 이 파일은 추적하지 말라고 알려주는 목록
```
