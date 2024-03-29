# Git

Git Program 설치
Git 다운받아 설치한다.

## Git 명령어

Help : git help config

## git 설정하기

사용자설정 : git config —global user.name “dldkffh”  
메일설정 : git config —global user.mail “jjaimsae@gmail.com”  
config확인  
git config —list  
git config user.name  
최초 설정 확인 : git config —show-origin user.name  
End of Line  
시스템설정대로 : git config —global core.eof native  
시스템설정대로 : git config —global core.autcrlf false  
Diff 결과 Highlighting 하기 : git config -global pager.diff ‘diff-highlight | less’  


## 로컬저장소만들기 
```powershell
mkdir project  
cd project
git init
git add *.c
git commit -m “My first version managing directory”
```


## 저장소 내려받기
```powershell
git clone id@원격저장소_URL
git clone /로컬저장소/저장소
```
File 상태 확인(Tracked : Modified/Unmodified/Staged, Untracked : Unstaged)

git status
git status -s :
: OO filename
: First O - Staging 상태를 보여줌
: Second O - Working directory 상태를 보여줌
: M - Modifyed
: A - Added
: ? - Unstaged
Staging Area file을 Unstage로 변경하기
git reset HEAD filename
git checkout — filename
Tag : 특정 commit에 대해 Tag를 지정 (Version 관리로 주로 사용)

### 조회
```powershell
git tag
git tag -l v1.4
git show v1.4
```

### 만들기
```powershell
LghtWeight : git tag v1.5
Annoated : git tag -a v1.5 -m “Version Updated by MC”
이전 commit에 tag 달기 : git tag -a 1.5 commithash
지우기 : git tag -d v1.5
Tag 공유하기 : git push origin v1.5
```

### Branch
```powershell
git branch -v
git branch —merged
git branch —no-merged
만들기 : git branch issues
변경하기 : git checkout issue
만들고 변경하기 : git checkout -b issue
확인하기 : git branch
삭제하기 :
Merged branch : git branch -d issue
No-merged brnach : git branch -D issue
파일만들기 : touch test.txt

파일추적하기 : git add test.txt
파일추적제외하기 : .gitignore 파일에 해당 파일명이나 filter를 적는다.
: *.[oa] - 확장자가 .o 이거나 .s는 무시한다.
```
### Commit

파일변경완료 : git commit -m “add test.txt”
Unstaged file를 바로 commit하기 : git commit -a -m “Version update”
diff결과를 commit message로 사용하기 git commit -v
이전 commit 지우고 새로 등록하기
git commit -m ‘initial commit’
git add forgotten_file
git commit —amend
Commit hash 확인하기 : git log —pretty=oneline
조회하기

git log
git log —pretty=format:”%h %s” —graph
원격저장소

원격저장소 확인하기
git remote -v
git remote show origin
원격저장소 내려받기 : git clone 원격저장소_URL
원격저장소 추가하기 : git add remote origin 저장소이름 원격저장소_URL
Fetch

git fetch origin
Merge

git checkout master
git diff orign master
git merge issue
git branch -d issue
원복하기

파일 원복 : git checkout — filename
Commit 원복
git fetch origin
git reset —hard origin/master
Pull(Fetch + Merge) : git pull

Push : git push origin issue

master로 merge 하고 Pull request 보내기 : 비추천 방식

master branch로 이동 : git checkout master
Merge : git merge issue
Push : git push origin/master master
issue로 pull request 보내고 master로 Pull 하기 : 추천 방식

push : git push origin issue
git request-pull origin issue
git checkout master
git fetch
git merge
Pull Request 보내기 : git request-pull origin/master issue

<br /><br />

출처: [밤소의 잠못드는 밤 IOT 이야기](https://midnightcow.tistory.com/135)



