# Git

아아아

> Gir은 분산형버전관리시스템(DVCS) 중 하나이다.



## 0. Git 기초설정

* windows 환경에서는 `git for windows`  로 검색해 `git bash`설치한다.  [다운로드링크](https://gitforwindows.org/)

* 최초에 컴퓨터에서 git 사용하는 경우 아래의 설정을 진행한다.

  ```bash
  $ git config -- global user.email '이메일주소'
  $ git config -- global user.name '이메일주소'
  #확인
  $ git config -- global -l
  ```

  * 이메일주소 설정할때 github에 가입된 이메일로 설정을 해야 커밋 이력이 github에 기록된다.



## 1. Git을 통한 버전관리 기본 흐름

### 1.1 Git 저장소 초기화

> 특정 폴더를 git 저장소로 활용하기 위해서 최초에 입력하는 명령어

``` bash
$ git init
Initialized empty Git repository in C:/Users/student/Desktop/媛뺤쓽/GIT?밴컯/TIL/.git/
```

* .git폴더가 숨긴폴더로 생성되며, git bash에서는 (master)라고표기된다.
  * 상위폴더 잘못 지정했을때 -> `.git`지워준다. 
  * 확인 방법 1. 배쉬를 켰는데 마스터가 벌써 써있어! - 잘못했다.

## 1.2 `add`

> 커밋 대상 파일들을 추가한다.

`add`전 상황

```bash
$ git status
On branch master

No commits yet#커밋 없음.
#트랙킹되지않는파일들
#=> 새로 생성된 파일이고, git으로 관리중이지 않는 파일.
Untracked files:
	# git add 파일
	# 밑에 친절하게 나와있요. 커밋될것들퐘시키기위해명령어써라
  (use "git add <file>..." to include in what will be committed)
        git.md
        markdown-images/
        markdown.md

nothing added to commit but untracked files present (use "git add" to track)
```

```bash
$ git add . 
$ git status
On branch master

No commits yet

Changes to be committed: #커밋 될 변경사항들.
  (use "git rm --cached <file>..." to unstage)
        new file:   git.md
        new file:   "markdown-images/\353\213\244\354\232\264\353\241\234\353\223\234.jpg"
        new file:   markdown.md

```

* add 명령어는 아래와 같이 활용된다.

  ```bash
  $ git add . #current dir whole
  $ git add git.md markdown.md # two files
  $ git add mardown-images/ # a directory
  ```

### 1.3 `commit`

> 이력을 확정짓는 명령어

```bash
$ git commit -m 'hola randomMSG'
[master (root-commit) f99cc1e] hola
 3 files changed, 96 insertions(+)
 create mode 100644 git.md
 create mode 100644 "markdown-images/\353\213\244\354\232\264\353\241\234\353\223\234.jpg"
 create mode 100644 markdown.md

$git status
On branch master
nothing to commit, working tree clean

```

`log`

> 커밋 내역을 확인할 수 있는 명령어

```bash
#log보기
$ git log
commit f99cc1e559457132cc745bd5101d1e702ba853a0 (HEAD -> master)
Author: seunghyunmoon2 <dktlfkrldh@gmail.com>
Date:   Wed Jul 8 14:42:35 2020 +0900

    hola
    
# 최근 n개 이력#(1개)
$ git log -1
commit f99cc1e559457132cc745bd5101d1e702ba853a0 (HEAD -> master)
Author: seunghyunmoon2 <dktlfkrldh@gmail.com>
Date:   Wed Jul 8 14:42:35 2020 +0900

    hola

#간략한 표현
$ git log --oneline
f99cc1e (HEAD -> master) hola

# 최근 n개 이력을 간략하게
$ git log --oneline -1
f99cc1e (HEAD -> master) hola

```



# 2. 원격 저장소 활용

> remote repository 제공 서비스 많다. (gitlab, bitbucket)
>
> github기준으로설명

## 2.1 원격저장소 등록

> git아! 원격저장소로(remote) 등록해줘(add) origin이라는 이름으로 URL을!

```bash
$ git remote add origin 저장소url
# https://github.com/seunghyunmoon2/GITClass.git
```

* 저장소확인

* ```bash
  $ git remove -v
  origin https://github.com/eunghyunmoon2/GITClass.git (fetch)
  origin https://github.com/eunghyunmoon2/GITClass.git (push)
  ```

* 저장소 삭제

  ```bash
  #origin으로 지정된 장소를 rm한다.
  $ gir remote rm origin
  ```

## 2.2  PUSH

origin으로 설정된 원격저장소의 master 브랜치로 push한다.

```bash
$ git push origin master
```



> 폴더가 올라가는게 아니고. 커밋한 버전만 따로 올라간다. -> 버전관리 따로따로 가능.



## 2.3 git 활용 예시

`clone`   (`init`)이랑 같게 생각하라.

> 원격저장소복제

```bash
~/집 $ git clone https://github.com/seunghyunmoon2/GITClass.git
#repository
Cloning into 'GITClass'...
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 6 (delta 0), pack-reused 0
Unpacking objects: 100% (6/6), 33.44 KiB | 187.00 KiB/s, done.

~/집 cd GITCLASS
~/집 /GITClass (master) $
```

* 복제하는경우 원격저장소이름의 폴더가 생성괸다.
* 해당폴더로이동하여활용(작업)

집에서작업하고

add, commit, push 한다~



### `pull`

* 다시멀캠에서 - remote의 변경사항 받아온다.

  ```bash
  ~/Desktop/TIL (master) $ git pull origin master
  ```

  



## 주의사항

> 원격저장소와 로컬의 이력이 다르게 구성고디는경우 
>
> 1) github에서 직접수정
>
> 2)협업과정
>
> 3)집-강의장환경왔다갔다하는상황발생가능오류

* 원격커밋목록과 로컬 `git log --oneline`하면 다른게있다.





* ㅇㅇ
  * Vim 편집기 -> 커밋메시지작성할수있는곳	
    * `esc`누르고 `:wq`순서대로 입력한다.
* 