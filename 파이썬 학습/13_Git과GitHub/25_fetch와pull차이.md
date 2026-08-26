# git fetch와 git pull 차이

둘 다 원격 저장소의 변경사항을 확인할 때 쓰지만 동작이 다르다.

## git fetch

```powershell
git fetch
```

원격 저장소에 새 커밋이 있는지 가져와서 **정보만 갱신**한다.

내 작업 파일을 바로 바꾸지는 않는다.

쉽게 말하면:

```text
fetch = 새 소식만 받아오기
```

## git pull

```powershell
git pull
```

원격 저장소의 변경사항을 가져오고 내 현재 브랜치에 반영하려고 한다.

쉽게 말하면:

```text
pull = 새 소식 받아오고 내 작업에도 합치기
```

## 차이를 그림처럼 보면

```text
GitHub 원격 저장소
       ↓ fetch
원격 정보만 갱신

GitHub 원격 저장소
       ↓ pull
내 현재 브랜치에도 반영
```

## 언제 fetch를 쓰나?

바로 합치기 전에 원격에 뭐가 바뀌었는지 먼저 확인하고 싶을 때 좋다.

```powershell
git fetch
git status
```

필요하면 로그도 확인한다.

```powershell
git log --oneline --all --graph
```

## 언제 pull을 쓰나?

팀원이 올린 최신 내용을 바로 내 브랜치에 받아와야 할 때 자주 쓴다.

```powershell
git pull origin main
```

## 초보자가 기억할 한 줄

```text
fetch = 확인 위주
pull = 가져와서 반영
```

단, 로컬에서 같은 파일을 수정해 둔 상태라면 `git pull`이 충돌하거나 중단될 수 있다. 그래서 팀 작업에서는 먼저 `git status`를 보는 습관이 좋다.
