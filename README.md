# git 내용 정리


### 2.1 Git 저장소 만들기
다음 두가지 방법으로 Git 저장소 사용 가능
- 로컬 디렉토리 선택해서 적용 (적용할 디렉토리에서 git init)
- clone 해서 사용 (git clone ***url***)

### 2.2 수정하고 저장소에 저장하기
- 파일 상태 확인 (git status)
- 파일 새로 추적 (git add ***file***)
- 변경사항 커밋 (git commit)
- 파일 삭제 (git rm ***file***)
- 파일 이름 변경 (git mv ***file***)

### 2.3 커밋 히스토리 조회하기
- 히스토리 조회하기 (git log)
시간 순으로 출력하고 각 커밋의 SHA-1 체크섬, 저자 이름, 저자 이메일, 커밋한 날짜, 커밋 메시지를 보여준다.
- 다양한 옵션 존재 (ex -p, --stat 등등)

### 2.4 되돌리기
- 완료한 커밋을 수정할때 (git commit --amend)
- unstaged 상태로 만들기 (git reset)
- 수정된 파일 되돌리기 (git checkout -- ***file***)
- 프로젝트 공유할때 (git push ***리모트 저장소 이름, 브랜치 이름***)

### 2.5 리모트 저장소
- 현재 프로젝트에 등록된 리모트 저장소 확인 (git remote)
- 리모트 저장소에서 데이터 가져오기 (git fetch ***remote***)
- 리모트 저장소 이름 바꾸기 (git remote rename)
- 리모트 저장소 삭제하기 (git remote rm)

### 2.6 태그
- 

### 2.7 Git Alias

dsfsdfdf



# docker 내용 정리
