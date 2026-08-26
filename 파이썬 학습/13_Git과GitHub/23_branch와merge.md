# 23. branch와 merge

Git의 branch는 **본 작업과 떨어진 곳에서 따로 작업하는 가지**라고 생각하면 된다.

## 왜 branch를 쓰나?

`main`에서 바로 작업하다가 망가지면 복구가 귀찮다.

그래서 새 기능을 만들 때는 별도 branch에서 작업하고, 괜찮으면 나중에 main에 합친다.

## 현재 branch 확인

```bash
git branch
```

또는:

```bash
git branch --show-current
```

## 새 branch 만들면서 이동

```bash
git switch -c feature/login
```

뜻:

```text
git switch   → branch를 바꾼다
-c           → 새 branch를 만든다
feature/login → 새 branch 이름
```

## 작업 후 저장

```bash
git add .
git commit -m "Add login page"
```

## GitHub에도 올리기

처음 올릴 때:

```bash
git push -u origin feature/login
```

다음부터는 보통:

```bash
git push
```

이면 된다.

## merge란?

branch에서 만든 변경사항을 다른 branch에 합치는 것이다.

예를 들어 `feature/login` 작업을 main에 합치고 싶다면 먼저 main으로 이동한다.

```bash
git switch main
```

최신 내용을 받는다.

```bash
git pull
```

그다음:

```bash
git merge feature/login
```

## GitHub에서는 PR을 많이 쓴다

팀 작업에서는 직접 `git merge`보다 Pull Request를 만들어 리뷰 후 합치는 경우가 많다.

흐름:

```text
branch 만들기
↓
코드 수정
↓
commit
↓
push
↓
GitHub에서 Pull Request
↓
확인 후 merge
```

## branch 이름 예시

```text
feature/login
feature/data-check
fix/login-error
docs/readme-update
```

이름은 팀 규칙에 따라 다를 수 있다.

## `main`과 branch를 쉽게 생각하면

```text
main = 현재 공식 버전
feature/... = 작업 중인 복사본 같은 가지
merge = 작업 결과를 공식 버전에 합치기
```

branch를 완벽히 이해하려고 하기보다 직접 하나 만들고 파일 한 줄 수정한 뒤 commit, push 해보는 것이 가장 빠르다.
