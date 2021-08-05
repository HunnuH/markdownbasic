## 협업

- `github - setting  - collaborators `: 협업할 상대를 초대/승인을 해줘야 한다.
- `admin, write ,read`등의 권한 부여가 설정가능



### push & pull

- `rejected` : 다른 작업이 있는데  그것을 자신의 로컬로 가져오지 않았다
  - `pull`을 이용하여 그 작업을 가져온다
- `git mergetool` : 병합도구



### git pull & feth & 원격 브랜치

- `git feth > git merge FERCH_HEAD > commit > push`  =  `git pull > commit > push`
- `git pull` = `git fetch`
- `.git/FETCH_HEAD` =  원격저장소의 최근 merge한 내용 저장되있다.
- `git fetch; git merge FETCH_HED`  = 내용을 참고하여 가장최근에 fetch한내용을 merge시킨다
  - 기능상은 동일하지만 자동으로 해준다



