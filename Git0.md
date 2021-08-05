## GIT

> 분사형(Distibuted)으로 버전을 통해 코드를 관리하는 도구

> 버전을 통해 코드를 관리하는 도구



## SCM & DVCS

- SCM (Sorurce Code Management) : 코드 관리 도구
- VCS( Version Control System) : 버전 관리 도구
- DVCS(Distributed Version Control System) : 분산형 버전 관리 도구



## 왜 버전으로 관리하는가?

- 변경 이력 관리 :  변경 사항에 따라 구분하고 싶어서
- 특정 시점으로 복원  : 그 이전 데이터가 필요할 수 있어서



## GIT의 코드 관리 단위

> 디렉토리(폴더) 단위



### `git init`

특정폴더에서 git 프로젝트 시작

- 리포지토리 (repository) : git 으로 관리되는 폴더

- 참고 : 리눅스 시스템에서 `.`으로 시작되는 파일/폴더는 숨김 파일/폴더

  - ex) `.git`
    - 확인 방법 : `ls -a` 

- `git init` 직후의 변화

  - `(master)`표시
  - `.git `폴더

  ```
  ysh32@DESKTOP-AFA9ICI MINGW64 ~/git-practice (master)
  ```

  ``` 
  Initialized empty Git repository in C:/Users/ysh32/git-practice/.git/
  ```

  

### `git status`

git 상태 출력

- `git init`직후

  ```
  On branch master
  >master 브랜치에 있어요
  
  No commits yet
  > commit이 아직 없어요
  
  nothing to commit (create/copy files and use "git add" to track)
  >commit 할게 없어요(.git add로 추적 가능해여)
  ```

- `touch a. txt`직후

  ``` 
  Untracked files:
  >추적되지 않은 파일들이 있어요
  
  (use "git add <file>..." to include in what will be committed)
          a.txt (빨강)
  >  commit 될 것에 포함시키고 싶으시면 git add 를 사용하세요   
  
  nothing added to commit but untracked files present (use "git add" to track)
  >commit 하기 위해 추가된 것이 없어요. 추적되지 않는 파일은 있어요
  ```

- `git add a.txt` 직후

  ```
  Changes to be committed:
  > commit 할 변경 내역들이 있어요
  
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt(초록)
  >git rm 써서 무대에서 내릴 수도 있어요
  ```

- `git commit`직후

   ````
   nothing to commit, working tree clean
   >commit할게 없어요, 작업 폴더가 깔끔해요
   ````

  

### `git add [파일/폴더]`

파일 추적 시작 & staging  area에 폴더를 추가



## `git commit -m [메시지]`

현재 add된 파일들의 상태로 버전생성

- `git commit -m 'test'`

- 생애 첫 commit 일 경우

  ```
  Author identity unknown
  > 작자미상
  
  *** Please tell me who you are.
  >본인이 누군지 알려주세요
  
  Run
  >다음의 명령어를 실행해주세요
  
  git config --global user.email "you@example.com"
  >git아 설정 전역으로 해줘, 사용자.이메일 '내 이메일'
  
  git config --global user.name "Your Name"
  >git아 설정 전역으로 사용자.이름 '내이름'
  
  to set your account's default identity.
  Omit --global to set the identity only in this repository.
  
  fatal: unable to auto-detect email address (got 'ysh32@DESKTOP-AFA9ICI.(none)')
  
  ```

- `gir coomit`의 요소
  - `commit hash` : 숫자
  - 

## `git config`

설정값 출력

- git config --global user.email "  "

- git confing --global user.name "  "



설정값 설정

- git config --global user.email "ysh0806@kakao.com"
- git confing --global user.name "seung hun"



## `git log`

현재까지의 버전을 모두 출력

``` 
commit 0acb1f8d9bee7d3d5c866f3ed26acdf5dabe85a2 (HEAD -> master)
Author: seung hun <ysh0806@kakao.com>
Date:   Thu Aug 5 11:46:01 2021 +0900

    First commit
```

- `git log --oneline` : 한줄로 출력
- `git log --oneline -[숫자]` : 선택한 숫자만큼 출력





## `git backup`

원격 저장소에 로컬저장소의 코드를 업로드

`git remote` : 원격저장소 정보 출력

- `git remote add [이름 ] [주소]\ ` 

  - `git remote add origin https://github.com/HunnuH/git-practice.git`

- `git remote -v ` : 상세 정보 출력

  

### `git push`

원격저장소에 로컬저장소를 업로드

- `git push orgin master` :  

