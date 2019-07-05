#컨테이너 기술과 Docker의 개요
- Docker : 컨테이너 기술을 사용하여 애플리케이션의 실행 환경을 구축 및 운용하기 위한 플랫폼

###2. 1 컨테이너 기술의 개요
#####1. 컨테이너
+ 컨테이너 : 호스트 OS상에 논리적인 구획(컨테이너)을 만들고, 애플리케이션을 작동시키기 위해 필요한 라이브러리나 애플리케이션 등을 하나로 모아, 마치 별도의 서버인 것처럼 사용할 수 있게 만든 것
+ 호스트 OS의 리소스를 논리적으로 분리시키고, 여러 개의 컨테이너가 공유하여 사용
+ 오버헤드가 적기 때문에 가볍고 고속으로 작동
+ 서버 가상화 기술과의 차이
	+ 일반적 물리 서버 
		+ 하나의 OS 상에서 움직이는 여러 애플리케이션이 똑같은 시스템 리소스를 사용
		+ 디렉토리를 공유, 서버에 설정된 동일한 IP 주소로 통신
		+ 여러 애플리케이션에서 사용하고 있는 미들웨어나 라이브러리 버젼이 다른 경우 서로 영향을 받지 않도록 주의
	+ 컨테이너 기술
		+ OS나 디렉토리, IP 주소 등과 같은 시스템 자원을 마치 각 애플리케이션이 점유하고 있는 것처럼 보이게 할 수 있음
		+ 애플리케이션의 실행에 필요한 모듈을 컨테이너로 모을 수 있음
		+ 여러 개의 컨테이너를 조합하여 하나의 애플리케이션을 구축하는 마이크로 서비스형 애플리케이션과 친화성이 높음

#####2. 컨테이너 역사
+ FreeBSD Jail
	+ 프로세스의 구획화
	+ 네트워크의 구획화
	+ 파일 시스템의 구획화
+ Solaris Containers
	+ Solaris 존 기능
	+ Solaris 리소스 매니저 기능
+ Linux Containers(LXC)

# 
###2. 2 Docker의 개요
#####1. 프로그래머에게 Docker란?
+ Docker를 사용하여 개발한 어플리케이션의 실행에 필요한 모든 것이 포함되어있는 Docker이미지를 작성
+ 이식성(portability)

# 
###2. 3 Docker의 기능
#####1. Docker 이미지를 만드는 기능(Build)
+ Docker는 애플리케이션의 실행에 필요한 프로그램 본체, 라이브러리, 미들웨어, OS나 네트워크 설정등을 하나로 모아 이미지 생성
+ Docker 이미지 : 애플리케이션의 실행에 필요한 파일들이 저장된 디렉토리
+ Docker 이미지는 겹쳐서 사용 가능

#####2. Docker 이미지를 공유하는 기능(Ship)
+ Docker 이미지를 Docker 레지스트리에서 공유 가능
+ Docker Hub

#####3. Docker 컨테이너를 작동시키는 기능(Run)
+ Docker는 Linux 상에서 컨테이너 단위로 서버 기능을 작동
+ Docker 이미지로 여러개의 컨테이너 기동 가능
+ Docker는 이미 움직이고 있는 OS상에서 프로세스를 실행시키는 것과 거의 똑같은 속도로 실행 가능

#####4. Docker 에디션
+ Docker Community Edition(CE)
+ Docker Enterprise Edition(EE)
+ 지원 플랫폼
	+ 서버 OS용 : Ubuntu, Debian, CentOS, Fedora
	+ 퍼블릭 클라우드용 : Microsoft Azure
	+ 클라이언트 OS용 : Microsoft Windows 10, macOS
+ Docker 릴리스

#####5. Docker 컴포넌트
+ Docker Engine(Docker의 핵심 기능)
+ Docker Registry(이미지 공개 및 공유)
+ Docker Compose(컨테이너 일원 관리)
+ Docker Machine(Docker 실행 환경 구축)
+ Docker Swarm(클러스터 관리)

# 
###2. 4 Docker의 작동 구조
#####1. 컨테이너를 구획화하는 장치(namespace)
+ namespace :
	+ 한 덩어리의 데이터에 이름을 붙여 분할함으로써 충돌 가능성을 줄이고, 쉽게 참조할 수 있게 하는 개념
	+ 이름과 연결된 실체는 그 이름이 어떤 namespace에 속해 있는지 고유하게 정해짐
	+ namespace가 다르면 동일한 이름이라도 다른 실체로 처리

+ PID namespace
	+ 프로세스에 할당한 고유한 ID로 프로세스 격리
+ Network namespace
	+ 호스트 OS상에서 사용중인 포트가 있더라도 컨테이너 안에서 동일한 번호의 포트 사용 가능
+ UID namespace
	+ UID, GID를 namespace별로 독립적으로 가져 관리 권한을 다르게 부여
+ MOUNT namespace
	+ MOUNT 조작으로 namespace 안에 격리된 파일시스템 트리를 생성
+ UTS namespace
	+ namespace별로 호스트명이나 도메인명을 독자적으로 가질 수 있음
+ IPC namespace
	+ 프로세스 간의 통신 오브젝트를 namespace별로 독립적으로 운용

#####2. 릴리스 관리 장치(cgroups)
+ 자원을 여러 컨테이너가 공유하여 작동하기 때문에 control group기능으로 자원 할당등을 관리
+ cgroups는 계층 구조를 사용하여 프로세스를 그룹화하여 관리 가능

#####3. 네트워크 구성(가상 브리지/가상 NIC)
+ Docker 컨테이너와 외부 네트워크가 통신을 할 때는 가상 브리지와 호스트OS의 NIC에서 패킷을 전송하는 장치가 필요한데 NAPT기능을 사용
+ NAPT(Network Address Port Translation) : 하나의 IP주소를 여러 컴퓨터가 공유하는 기술
	+ IP주소와 포트 번호를 변환하는 기능
	+ TCP/IP의 포트 번호까지 동적으로 변환하기 때문에 하나의 글로벌 IP주소로 여러 대의 머신이 동시에 연결 가능

#####4. Docker 이미지의 데이터 관리장치
+ Copy on Write 방식으로 컨테이너 이미지를 관리
+ AUFS : 다른 파일 시스템의 파일이나 디렉토리를 투과적으로 겹쳐서 하나의 파일 트리를 구성할 수 있는 파일시스템
+ Btrfs : Linux용 Copy on Write 파일시스템으로 과거의 상태로 돌아갈 수 있는 롤백 기능이나, 어떤 시점에서의 상태를 저장할 수 있는 스냅샷 기능 포함
+ Device Mapper : 파일 시스템의 블록I/O와 디바이스의 매핑 관계를 관리
+ OverlayFS : 파일 시스템에 다른 파일 시스템을 투과적으로 머징하는 장치
+ ZFS : 볼륨 관리, 스냅샷, 체크섬 처리, 리플리케이션 등을 지원
