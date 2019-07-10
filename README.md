# git 내용 정리

## 2 Git의 기초

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
- 태그 조회하기, 생성하기
- 태크 종류 (lightweight, annotated)

### 2.7 Git Alias
- config 사용하여 각 명령의 alias 쉽게 만들 수 있다.

## 3 Git 브랜치

### 3.1 브랜치란 무엇인가
- 브랜치란 커밋 사이를 가볍게 이동할 수 있는 포인터 같은 것
- 처음 커밋하면 master 브랜치(기본)거 생성된 커밋을 가리킨다.
- 새 브랜치 생성 (git branch ***name***)
- 브랜치 이동하기 (git checkout ***name***)
- git log로 정보 확인 가능

### 3.2 브랜치와 Merge의 기초
- merge의 진행 방식은 다음과 같다.
- 작업 진행 -> 새로운 이슈 처리할 새 branch 생성 -> 새 branch에서 작업 진행 -> 이전 브랜치에서 merge 진행

### 3.3 브랜치 관리
- 브랜치 목록 확인 (git branch)
- -v 사용하면 커밋 메시지 확인가능
- -d 명령으로 삭제 가능

### 3.4 브랜치 워크플로
- 배포한 코드는 master 브랜치에 두고 개발을 진행하거나 안정화하는 브랜치는 추가로 따로 브랜치를 만들어서 관리한다.
- 테스트를 거쳐서 안정적이라 판단하면 해당 브랜치를 master 브랜치와 merge 하는 원리

### 3.5 리모트 브랜치
- 리모트 트래킹 브랜치 일종의 북마크 같은 역할 (로컬에 있지만 임의로 움직일 수 없음)
- 리모트 트래킹 브랜치의 이름은 remote/branch 형식
- git fetch로 서버의 데이터 내려받을 수 있음
- 리모트 트래킹 브랜치를 로컬 브랜치로 checkout하면 자동으로 트래킹 브랜치 만들어짐
- git pull 명령은 fetch 명령 이후에 merge 명령을 실행하는 것일 뿐이다.

### 3.6 Rebase 하기
- 변경된 사항을 patch로 만들고 이를 원래에 다시 적용시키는 방식
- git checkout... -> git rebase... 식으로 실행
- merge와는 달리 히스토리가 깔끔해진다. merge와 기능은 같다.
- 주의) 공개 저장소에 push한 커밋을 rebase 하면 코드가 엉키게 된다.

## 6 GitHub

### 6.1 계정 만들고 설정하기

### 6.2 GitHub 프로젝트에 기여하기
- 프로젝트 fork 하기 (프로젝트를 통째로 복사해준다)
- pull request (push 한 변경 내용을 원래 저장소로 보내는 것)
1.Fork 한 개인 저장소를 로컬에 Clone 한다.
2.무슨 일인지 설명이 되는 이름의 토픽 브랜치를 만든다.
3.코드를 수정한다.
4.잘 고쳤는지 확인한다.
5.토픽 브랜치에 커밋한다.
6.GitHub의 개인 저장소에 토픽 브랜치를 Push 한다.
- pull request는 토론을 통해 결정

### 6.3 GitHub 프로젝트 관리하기

### 6.4 Organization 관리하기

### 6.5 GitHub 스크립팅
- 서비스 (설정하면 누군가 저장소에 push 할 때마다 이메일이 날라감, 다양한 이벤트 처리가능, 보통은 push 할 때 그 데이터를 가지고 한다.)
- 훅 (서비스에 없는 사이트나 외부 서비스와 연동하고 싶을 때 사용, url로 http 페이로드를 보내줌)
- API (API에 연결하면 이슈에 코멘트하고, pull request의 상태 변경 등 가능)


# docker 내용 정리

## 1 시스템과 인프라 기초 지식

### 1.1 시스템 기반의 기초 지식
- 시스템 기반의 구성 요소
  - 하드웨어
    - 시스템 기반을 구성하는 물리적인 요소
  - 네트워크
    - 원격지에서 액세스 할 수 있도록 서버들을 연결
  - OS (운영체제)
    - 하드웨어나 네트워크 장비를 제어하기 위한 기본 소프트웨어
  - 미들웨어
    - OS 상에서 서버가 특정 역할을 하기 위한 기능을 갖고 있는 소프트웨어
    
- 클라우드와 온프레미스
  - 온프레미스
    - 자사에서 데이터센터를 보유하고 모든 과정을 수행하는 형태
  - 퍼블릭 클라우드
    - 인터넷을 통해 불특정 다수에게 제공되는 클라우드 서비스
  - 프라이빗 클라우드
    - 특정 그룹에게만 제공되는 클라우드 서비스

- 시스템 기반의 구축/ 운용 흐름
  - 시스템화 계획 요구사항 정의 -> 인프라 설계 -> 인프라 구축 -> 운용
  
### 1.2 하드웨어와 네트워크 기초 지식
- 서버 장비
  - CPU
    - 프로그램의 설계나 처리를 수행하는 전자회로 부품
  - 메모리
    - CPU가 직접 액세스 할 수 있는 기억장치
  - 스토리지
    - 데이터베이스에 기록하는 데이터 등과 같은 영구적인 데이터를 저장하는 디바이스
  
- 네트워크 주소
  - MAC 주소 (물리 주소, 이더넷 주소, 16진수로 표기)
  - IP 주소 (네트워크 장비에 할당되는 식별 번호, 10진수 4개를 나열하여 나태냄)
  
### 1.3 리눅스(OS) 기초 지식
- 리눅스 커널
  - 리눅스 커널은 하드웨어 제어에 관한 OS의 핵심이 되는 기능을 말하는 것
  - 주요 기능
    - 디바이스 관리
    - 프로세스 관리
    - 메모리 관리

### 1.4 미들웨어 기초 지식
- 웹 서버
  - 클라이언트의 브라우저가 보내온 HTTP의 요청을 받아, 웹 콘텐츠를 응답으로 반환하거나 다른 서버사이드 프로그램을 호출하는 기능을 가지고 있는 서버
- 데이터베이스 서버
  - 시스템이 생성하는 다양한 데이터를 관리하기 위한 미들웨어
- 시스템 감시 툴
  - 시스템이 안정적으로 가동되는지 감시

### 1.5 인프라 구성 관리 기초 지식
- 인프라 구성 관리
  - 인프라를 구성하는 하드웨어, 네트워크, OS, 미들웨어, 애플리케이션의 구성 정보를 관리하고 적절한 상태로 유지하는 작업

- 대표적인 인프라 구성 관리 툴
  - KickStart, Vagrant, Chef, Puppet, Kubernetes 등

- 지속적 인티그레이션
  - 애플리케이션의 코드를 추가 및 수정할 때마다 테스트를 실행하고 확실하게 작동하는 코드를 유지하는 방법

- 지속적 딜리버리
  - 모든 기능을 한 번에 다 만드는 것이 아니라 기능을 추가할 때마다 애플리케이션을 제품 환경에 배포하는 방법

## 2 컨테이너 기술과 Docker의 개요

### 2.1 컨테이너 기술의 개요
- 컨테이너
  - 호스트 OS상에 논리적인 구획을 만들고 애플리케이션을 작동시키기 위해 필요한 라이브러리나 애플리케이션 등을 하나로 모아 별도의 서버인 것처럼 활용

### 2.2 Docker의 개요
- 애플리케이션의 실행에 필요한 환경을 하나의 이미지로 모음
- 이미지를 사용하여 다양한 환경에서 애플리케이션 실행 환경을 구축 및 운용
- 오픈 소스 플랫폼, 내부에서 컨테이너 기술을 사용
- 도커는 인프라 환경을 컨테이너로 관리

### 2.3 Docker의 기능
- 도커 이미지를 만드는 기능
  - 애플리케이션 실행에 필요한 파일들이 저장된 디렉토리
- 도커 이미지를 공유하는 기능
  - 도커 레지스트리에서 공유가능(도커 허브)
- 도커 컨테이너를 작동시키는 기능
  - 도커는 컨테이너 단위로 서버 기능을 작동(이미지 필요)
  - 도커는 컨테이너를 독립된 공간으로서 관리

### 2.4 Docker의 작동 구조
- 컨테이너를 구획화하는 장치(namespace)
  - namespace : 한 덩어리의 데이터에 이름을 붙여 분할함으로써 충돌 가능성을 줄이고, 쉽게 참조할 수 있게 하는 개념
  - 리눅스 커널의 namespace 기능은 리눅스의 오브젝트에 이름을 붙여 총 6개의 독립된 환경 구축 가능
 
- 릴리스 관리 장치
  - 도커는 리눅스 커널의 기능인 'control groups' 기능을 사용하여 자원의 할당 등을 관리
  - 컨테이너 안의 프로세스에 대해 그룹별로 제한을 둘 수 있다.
  - 프로세스를 그룹화하여 관리 가능
  
- 네트워크 구성
  - 가상 브리지 / 가상 NIC 이용
 
- 도커 이미지의 데이터 관리 장치
  - Copy on Write 방식으로 컨테이너의 이미지를 관리
  
## 3 Docker 설치와 튜토리얼
### 3.1 Docker 설치와 작동 확인
### 3.2 웹 서버를 작동시켜 보자

## 4 Docker 명령
### 4.1 Docker 이미지 조작
### 4.2 Docker 컨테이너 생성/시작/정지
### 4.3 Docker 컨테이너 네트워크
### 4.4 가동 중인 Docker 컨테이너 조작
### 4.5 Docker 이미지 생성

## 5 Dockerfile을 사용한 코드에 의한 서버 구축
### 5.1 Dockerfile을 사용한 구성 관리
### 5.2 Dockerfile의 빌드와 이미지 레이어
### 5.3 멀티스테이지 빌드를 사용한 애플리케이션 개발
### 5.4 명령 및 데몬 실행
### 5.5 환경 및 네트워크 설정
### 5.6 파일 설정

## 6 Docker 이미지 공개
### 6.1 Docker 이미지의 자동 생성 및 공개
### 6.2 Docker Registry를 사용한 프라이빗 레지스트리 구축
### 6.3 클라우드 서비스를 사용한 프라이빗 레지스트리 구축

## 7 여러 컨테이너의 운용 관리
### 7.1 여러 컨테이너 관리의 개요
### 7.2 웹 애플리케이션을 로컬에서 움직여 보자
### 7.3 Docker Compose를 사용한 여러 컨테이너의 구성 관리
### 7.4 Docker Compose를 사용한 여러 컨테이너의 운용
