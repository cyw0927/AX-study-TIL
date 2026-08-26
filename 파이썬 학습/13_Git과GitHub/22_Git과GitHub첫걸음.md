# 22. Git과 GitHub 첫걸음

Git과 GitHub는 이름이 비슷해서 처음에 같은 것으로 생각하기 쉽다. 하지만 역할이 다르다.

```text
Git = 내 컴퓨터에서 파일 변경 기록을 관리하는 도구
GitHub = 그 기록과 파일을 인터넷에 올려 공유하는 서비스
```

## 가장 먼저 보는 단어

### repository

프로젝트 폴더라고 생각하면 된다. 줄여서 `repo`, 한국어로는 저장소라고 많이 부른다.

### commit

현재 변경 내용을 하나의 기록으로 남기는 것이다.

게임에서 세이브 포인트를 만드는 것과 비슷하다.

### push

내 컴퓨터의 commit을 GitHub에 올린다.

### pull

GitHub에 있는 최신 내용을 내 컴퓨터로 가져온다.

### clone

GitHub 저장소를 처음 통째로 내 컴퓨터에 복사한다.

## 가장 기본적인 흐름

파일을 수정했다고 하자.

```text
파일 수정
↓
git status
↓
git add
↓
git commit
↓
git push
```

## `git status`

지금 어떤 파일이 바뀌었는지 확인한다.

```text
git status
```

Git을 쓰다가 헷갈리면 가장 먼저 실행해도 좋은 명령어다.

## `git add`

commit에 넣을 파일을 고른다.

```text
git add app.py
```

모든 변경 파일을 넣으려면:

```text
git add .
```

여기서 점 `.`은 현재 폴더 아래의 변경 내용을 뜻한다고 생각하면 된다.

## `git commit`

선택한 변경 내용을 기록한다.

```text
git commit -m "로그인 화면 수정"
```

`-m` 뒤에는 이번에 무엇을 바꿨는지 짧게 적는다.

## `git push`

commit을 GitHub로 올린다.

```text
git push
```

처음 만든 branch라면 다음처럼 더 긴 명령을 볼 수도 있다.

```text
git push -u origin main
```

## `git pull`

GitHub의 최신 파일을 내려받아 현재 작업 폴더에 반영한다.

```text
git pull
```

팀원이 먼저 수정한 내용이 있을 때 특히 중요하다.

## `git clone`

저장소를 처음 받아올 때 사용한다.

```text
git clone 저장소주소
```

이미 clone한 폴더 안에서 또 clone할 필요는 없다. 이미 받은 저장소를 최신으로 만들고 싶으면 보통 `git pull`을 사용한다.

## branch

원본 작업을 바로 건드리지 않고 옆길을 하나 만들어 작업하는 기능이다.

```text
git switch -c feature/login
```

새 `feature/login` branch를 만들면서 이동한다.

현재 branch 확인:

```text
git branch --show-current
```

## fetch와 pull의 차이

처음에는 이렇게 기억하면 된다.

```text
git fetch = GitHub에 뭐가 바뀌었는지 가져오기만 함

git pull = 가져오고 내 현재 작업에도 반영함
```

즉 pull이 더 적극적으로 내 파일에 영향을 준다.

## 자주 생기는 상황

### push가 안 된다

먼저:

```text
git status
git branch --show-current
```

를 확인한다.

### pull이 안 된다

내 컴퓨터에 아직 commit하지 않은 수정 사항이 GitHub 변경과 충돌할 수 있다. 이때 오류 메시지를 읽고 무작정 명령어를 여러 개 치지 않는 것이 중요하다.

### GitHub에는 있는데 내 컴퓨터에는 없다

```text
git pull
```

을 먼저 생각한다.

## 초보용 최소 명령어

```text
git status
git add .
git commit -m "수정 내용"
git push
git pull
git branch --show-current
```

이 여섯 개를 실제로 여러 번 써보는 것이 처음부터 Git 전체를 외우는 것보다 낫다.
