# Git (혼자서 작업하기)

## 1. Git 기초

### 커밋(commit)
- 게임의 `세이브`에 해당하는 행동
    - 커밋을 해야 세이브가 된다.
- 다시말해 언제든지 커밋한 시점으로 돌아 갈 수 있다.
- 커밋을 하려면 `저장을 원하는 파일들을 묶어서` 커밋 명령을 수행하면 된다.

#### 커밋 주의사항
1. 반드시 한 번에 하나의 논리적 작업만을 커밋한다.
2. 커밋 메시지는 잘 적어야 한다.

##### 커밋 메시지 작성법
1. 첫 줄에 간단하지만 명확한 내용을 쓴다.
2. 한 줄 비우고
3. 자세한 내용을 적는다.

### 스테이지에 올린다(add)
- commit에서 `저장을 원하는 파일을 묶는` 작업이 필요하다고 했다.
- 이 작업을 `스테이지에 파일을 올린다`라고 한다.

### github에 업로드(push)
- 커밋을 하면 현재 작업 내용의 데이터가 내 컴퓨터(로컬)에 저장된다.
- 이 것을 Github에 업로드하는 걸 push라고 한다.

### (가장 간단한) 일련의 절차
1. Github에서 repository 생성
2. 해당 repo URL 복사
3. Git client(sourcetree, GitKraken, terminal ...) setup
4. 설치한 Git client App에서 복사한 URL Clone
    - Clone : 원격 저장소의 내용을 내 컴퓨터(로컬)로 복사
5. 작업 진행
6. git add
    - add : 로컬에서 작업한 파일들을 스테이지에 추가
7. git commit
    - commit : 스테이지에 올라온 파일들을 가지고 내 로컬에 저장(세이브)
8. git push
    - push : 커밋들을 원격 저장소에 업로드

## 2. 스테이지에 올리지 않은(add 명령 하기 전) 변경사항 취소하기
- `chekout`
    - checkout 명령을 통하여 마지막 커밋으로 되돌아 갈 수 있다.
    - `$ git checkout .` : repository 내 모든 수정 되돌리기
    - `$ git checkout {dir}` : 특정 디렉토리 아래 모든 수정 되돌리기
    - `$ git checkout {filename}` : 특정 파일의 수정 되돌리기
- sourceTree의 `코드뭉치 버리기`(마지막 커밋으로 되돌아 가고 싶을때 사용) 기능을 사용하면 변경사항을 되돌릴 수 있다.

## 3. 브랜치의 개념
- 이미 돌아가고 있는 프로그램에서 기능을 바꾸고 싶은 일이 생길 수 있다. 그럴 때 어떻게 해야 하나? 보통 초보 개발자들은 주석을 활용한다. 돌아가고 있는 부분을 삭제하면 아까우니까 주석 처리하고 개발한다.
- 이렇게 시간이 지나면서 코드가 엉망진창이 되버리는데 이런 상황을 막기 위해 브랜치를 사용한다.
- 브랜치란 : 가상의 작업 환경
    - 브랜치를 생성하면 기존의 마스터 브랜치의 내용은 그대로 보존하면서 새로운 작업 환경을 생성한다.(기존 내용을 유지한 체 새로운 내용을 추가하고 싶을 때 사용 = 특정 브랜치(혹은 커밋) 으로 돌아가고 싶을 때)
-  소스트리로 예를 들면 해당 커밋에서 우클릭 -> 브랜치 -> 새 브랜치를 통해 브랜치를 생성한다. = `checkout`
    - 소스트리에서는 해당 브랜치 더블 클릭으로 쉽게 체크 아웃 가능.
- 명령어 : `$ git branch [옵션] [브랜치명 A] [브랜치명 B]`
- 깃에서는 한 번에 하나의 브랜치에서만 작업 가능하다. 이를 헤드(HEAD) 브랜치(현재 작업 중인 브랜치) 라고한다.

## 4. 브랜치 병합하기

### 병합이란?
- 하나의 브랜치를 현재 브랜치와 합치는 것을 병합(merge)라고 한다.
- 현재 브랜치는 헤드(HEAD) 브랜치라고 한다고 했다.
- 예를 들어 헤드 브랜치아 master 이고 여기서 version2 브랜치를 병합하면 version2의 내용이 master에 반영되게 된다.

### 상황1. 헤드 브랜치에 변경 사항이 없을 경우 : fast forwad

1. 합치려는 브랜치가 헤드 브랜치로부터 시작되었다.
2. 그 사이 헤드 브랜치에는 전혀 갱신이 없었다.
- 주로 혼자 작업할 때 발생하는 상황
- 단순히 브랜치의 참조만 갱신되는 상황
- [git branch 연습 사이트](https://learngitbranching.js.org/)\

```shell
$ git commit
$ git barnch version2
$ git checkout version2
$ git commit
$ git commit
$ git checkout master
$ git merge version2
```

### 상황2. 가지가 생겨난 경우

1. 과거의 커밋으로부터 브랜치를 생성해서 작업을 한 경우
2. 새로운 브랜치 작업 이후에 헤드에 다른 새 커밋이 있는 경우
3. 여러 브랜치를 동시에 작업하면서 병합을 시도할 경우

```shell
$ git commit
$ git brach version2
$ git brach version3
$ git checkout version2
$ git commit
$ git commit
$ git checkout version3
$ git commit
$ git commit
$ git checkout master
$ git merge version3
$ git merge version2
- 충돌 가능성이 있다.(conflict) : 수동 해결
```

- 충돌 무섭지 않다! `에러 메시지 꼭 확인`
- 소스트리의 경우 헤드 브랜치에서 병합할 브랜치의 커밋 메시지 우클릭 -> 병합

## 5. pull 및 충돌 해결하기

### git pull
- 서버의 내용이 최신을 경우 pull 적용
- pull = fetch(원격저장소의 변경사항 가져와서 원격브랜치를 갱신) + merge

### 안쓰는 브랜치 삭제하기
- 현재 브랜치(HEAD)가 아닌 경우 (이미 Merge가 된 경우) 간단하게 삭제 가능

### 충돌의 발생 원인
- 자동병합을 실패했을 경우
- 주로 두 커밋이 같은 파일을 편집했을 경우 발생

### 해결법
- 에디터를 이용한 해결
    - 수동으로 수정
- 병합툴을 이용한 해결(diff tool)
- sourceTree를 이용한 해결
    - 내 것 또는 저장소 것 선택하기

## 6. 이전 커밋으로 되돌리기(reset)
- 소스트리의 `이 커밋까지 현재 브랜치를 초기화(Reset current branch to this commit)`버튼 
- `git reset --hard [commit hash 값]` 에 해당하는 명령으로 커밋을 되돌리기 (soft, mixed는 개별적으로 알아보기)
    - 원격 저장소에 올려져 있지 않은 이전 커밋은 사라짐
- reset 이후 push는 force 옵션을 선택해야 함
    - 원격저장소에 저장된 이전 커밋 사라짐
        - 따라서 유지하려면 reset을 한 후 원격저장소의 커밋과 merge를 한 후에 push를 해주면 --force를 사용하지 않아도 된다.
- push --force 는 소스트리에서 지원하지 않기 때문에 CLI를 이용해야 함
- reset은 Commit이 없어질 가능성이 굉장히 높으므로 권장하지 않음

### reset의 장.단점
- 장점: 쉽다.
- 단점: 커밋이 날아간다. push --force 가 필요하다.

## 7. 이전 커밋으로 되돌리기 (checkout, 브랜치를 만들어서 커밋 되돌리기)
- 혼자서 작업할 시 가장 추천하는 방법
- 설명
    - 되돌릴 커밋 대상으로 브랜치 생성
    - 체크아웃
    - 작업 후 커밋
    - master 브랜치에서(master로 checkout) 이전에 작업한 커밋 merge & push
    - 작업 완료한 브랜치는 삭제

### checkout의 장.단점
- 장점 : 쉽다. reset과는 달리 내용이 사라지지 않는다. (기록이 다 남아 있다.), 강제 push 필요하지 않음
- 단점 : 트리가 지저분해진다.

 ## 8. 이전 커밋으로 되돌리기 (Revert)
 - 커밋을 보존하면서 작업 디렉토리의 내용만 되돌릴 수 있는 방법. (커밋은 남기고 되돌리기)
 - 대상 커밋을 HEAD 커밋의 자식으로 새로 생성한다.
 - revert 대상 커밋은 사라지지 않는다.
 - revert 대상 커밋의 내용을 되돌린 `새로운 커밋이 생겨난다.`
 - 소스트리의 `커밋 되돌리기(reverse commit)`

```shell
$ git commit (C2)
$ git commit (C3)
$ git revert C3 (C2와 같은 C3*가 새로 생김)
```

 ### 장.단점
 - 장점 : 이전 커밋 기록이 다 남아 있다.
 - 단점 : 충돌 날 가능성이 매우 높다. 다소 어렵다.

 ## 9. Revert를 이용해 여러 커밋 되돌리기
- 최신부터 순서대로 revert를 반복 적용하면 된다.
 
 ![git-revert](/images/git-revert.PNG)

- 위 그림 설명
    1. commit 1 -> commit 2 -> commit 3 순으로 커밋이 진행됨.
    2. 가장 최큰 커밋(HEAD commit)인 commit 3에서 revert 진행(우클릭 -> 커밋 되돌리기) -> commit 2의 내용으로 돌아감. (여기 까지는 8번 이전 커밋으로 되돌리기에 해당)
    3. 그 다음 이전 커밋(commit 1)으로 되돌리고 싶으면 commit2에서 (우클릭 -> 커밋 되돌리기)를 진행하면 commit 1의 내용으로 돌아간다.
    
- 참고로 명령어를 사용하면 훨씬 쉽다.

```git
$ git revert HEAD HEAD~1 // 명령어 사용
```

- $ git revert HEAD (가장 최근 커밋을 되돌려라.)
- HEAD~1 : HEAD의 부모

## 10. stash를 이용한 작업 내용 저장

- 브랜치 체크아웃시 주의사항
    - 브랜치를 만들고 체크아웃을 하려면 현재 작업 디렉토리가 깨끗해야 한다.(`브랜치를 만들려면 마지막 커밋과 현재 작업 디렉토리의 내용이 같아야한다.`)
    - 그런데 갑작스럽게 체크아웃이 필요하다면?

### 첫번째 방법, 작업 중인 내용의 임시 저장
1. 브랜치 1에서 일단 (임시) 커밋을 한다.
2. 브랜치2로 체크아웃하고 볼 일을 본다...
3. 다시 브랜치1로 되돌아 온다.
4. 1의 작업을 이어서 마무리 짓는다.
5. `커밋 덮어쓰기 (commit --amend)` (소스트리 : 마지막 커밋 정정)를 한다.
6. (옵션) 필요하다면(이미 push 한 경우) (push --force)를 한다.

### (핵심) 두번째 방법, Stash를 이용해서 같은 작업 하기
1. Stash를 만든다.
2. 이 때 새로운 파일이 있었다면(신규 파일, untracked files) 일단 인덱스에 추가한다.
3. 체크아웃한다.
4. 되돌아 온다.
5. Stash 를 Pop한다!
6. 보통 커밋을 새로 생성한다.
- Stash : 다른 브랜치로 체크아웃하기 전에 현재 작업내용을 저장하는 임시 저장소

## 11. rebase 사용해서 트리 정리하기(히스토리 관리하기)
- Rebase 사용해 보기
    - 병합(merge) 처럼 두 브랜치를 합칠 때 사용한다.
    - 현재 브랜치가 대상 브랜치 위로 올라간다.
    - 소스트리에서는 "재배치"라는 명령이다.
        - 현재 브랜치에서 대상 브랜치에 우클릭하고 재배치(Rebase) 실행 
        - 충돌 시 수정 후 다시 한번 우클릭 재배치(Reabase) -> continue

 ### 장.단점
 - 장점 : 커밋 히스토리가 깔끔하게 정리된다.
 - 단점 : 잘못하면 위험하다. `이미 원격 저장소에 올라간 경우 + 협업을 하고 있는 경우 특히 위험하다.`
    - 깃에서도 원격 저장소에 올라간 경우 rebase를 사용하지 말라고 권고 


## Links
- [코드스쿼드 Git 입문 강의 : 정호영님](https://www.youtube.com/watch?v=8AtHcXnJSdA&t=0s&list=PLAHa1zfLtLiPrxoBo9a1HVmauvE2Mn3xX&index=2)