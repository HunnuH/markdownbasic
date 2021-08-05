# Git CLI 버전관리

- 버전관리의 시작

  - `git init  . ` : 해당 디렉토리를 버전관리를 시작할것

  - `init` : 초기화

  - `.` : 현재 디렉토리를 버전관리를 시킨다.

  - `.git `: 절대로 삭제 하지 말것

    ​            버전정보들이 저장되어 있음

  - `git reset --help` : 메뉴얼

  

- 버전생성

  - | working tree  | staging area           | repository    |
    | ------------- | ---------------------- | ------------- |
    | 수정한 파일들 | 버전을 만들려는 파일들 | 만들어진 버전 |

  - `cat` :  뒤의 파일을 화면에 출력

  - `git status` : 현재 git의 상태 출력

  - `commit` : 버전

  - `git add` : staging area 추가

  - `git commit` : 버전을 생성(기본에디터)

  - `git log` : 데이터정보 확인

  - `git add .` : 현재 디렉터리 밑의 모든 파일을 추가

  - `git commit -a " "` :  `"  "`를 `add와 coommit`을 한번에 한다

    - 주의 : `untracked`상태인것은 자동으로 `add`되지 않는다.

  - `git commit -m " "` : 커맨드라인에서 직접 `commit message`를 적을때 사용

  - `git config --global core.editor "  "` : 기본에디터 변경

    

- 오류

  - `untracked file` :  추적되지 않은 파일

  - `noting to commit` : 버전으로 생성할것이 없다

    

- 버전간의 차이점 비교
  -  `git diff` :  추가되거나 제거된 정보의 차이점을 확인
  - `git log -p`: 마지막 버전이후의 새로운 정보를 확인



- chek out
  -  `git chekout "commid id'`: id가 가리키는 버전을 만든 시점으로 돌아간다
  - `git chekout master`: 최신버전으로 되돌아간다



- 버전삭제
  - `git reset --hard " "`  : 해당(" ") 버전으로 되돌아간다.
  - `git reset  --hard` : 수정한 버전까지 삭제



- 버전 되돌리기
  - `git revert " "` : 해당(`" "`) 버전 이전으로 되돌아 간다 (단, 기존 commit 그대로 존재)
    - 주의 :  무조건 역순으로 순서대로 `revert` 해야한다.



