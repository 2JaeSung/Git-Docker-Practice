#Docker 설치와 튜토리얼

###3.1 Docker 설치와 작동 확인
#####1. Docker의 클라이언트 툴

+ Linux
	+ 설치 사전준비
`$ sudo apt-get update`
`$ sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common`
`$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
`$ sudo apt-key fingerprint 0EBFCD88`
`$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`
`$ sudo apt-get update`

	+ Docker 설치하기
`$ sudo apt-get install docker-ce`

+ Docker에서 'Hello world'
`$ docker container run ubuntu:latest /bin/echo 'Hello world'`

+ Docker 버전 확인(docker version)
`$ docker version`

+ Docker 실행 환경 확인(docker system info)
`$ docker system info`

+ Docker 디스크 이용 상황(docker system df)
`$ docker system df`

# 
###3.2 웹 서버를 작동시켜 보자
+ Docker 이미지 다운로드하기
	+ 이미지 다운로드
	`$ docker pull nginx`

	+ 이미지 확인
	`$ docker image ls`

+ Nginx를 작동시켜 보자
`$ docker container run --name webserver -d -p 80:80 nginx`

+ Nginx 작동 확인
	+ Nginx 서버의 상태 확인
	`$ docker container ps`
	+ 컨테이너 가동 확인
	`$ docker container stats webserver`

+ Nginx의 기동 및 정지
	`$ docker stop webserver`
	+ 컨테이너 기동
	`$ docker start webserver`
