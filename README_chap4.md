#Docker 명령

###4.1 Docker 이미지 조작
#####1. Docker Hub
+ [https://hubdocker.com](https://hubdocker.com)
	+ 공식 docker 이미지 : official
	+ [Repo Info] : Docker 이미지 상세 정보
	+ [Tags] 
	 `이미지명 [:태그명]`
	 - 태그명에 latest를 지정 가능

#####2. 이미지 다운로드(docker image pull)
+ `docker image pull [옵션] 이미지명[:태그명]`
+ -a : 모든 태그 이미지 취득
+ URL을 지정하여 이미지 취득 가능

#####3. 이미지 목록 표시(docker image ls)
+ `docker image ls [옵션] [리포지토리명]`
+ 옵션

|옵션 | 설명 |
| ---- | ---- |
| -all, -a |  모든 이미지를 표시 |
|--digests|다이제스트를 표시할지 말지
|--no-trunc|결과를 모두 표시|
|--quiet, -q| Docker 이미지 ID만 표시|
+ 결과

| 항목 | 설명 |
| ---- | ---- |
| REPOSITORY |  이미지 이름 |
|TAG|이미지 태그명
|IMAGE ID|이미지 ID|
|CREATED| 작성일|
|SIZE|이미지 크기

#####4. 이미지 상세 정보 확인(docker image inspect)
+ `docker image insepct 이미지명[:태그명]`

#####5. 이미지 태그 설정(docker image tag)
+ `<docker Hub 사용자명>/이미지명:[태그명]`

#####6. 이미지 검색(docker search)
+ `docker search [옵션] <검색 키워드>`
+ 옵션

옵션|설명
----|----
--no-trunc|결과를 모두 표시
--limit|n건의 검색 결과를 표시
--filter=stars=n|즐겨찾기의 수(n 이상)를 지정
+ 결과

항목|설명
---|---
NAME|이미지 이름
DESCRIPTION|이미지 설명
STARS|즐겨찾기 수
OFFICIAL|공식 이미지인지 아닌지
AUTOMATED|Dockerfile을 바탕으로 자동 생성된 이미지인지 아닌지

#####7. 이미지 삭제(docker image rm)
+ `docker image rm [옵션] 이미지명 [이미지명]`
+ 옵션

옵션|설명
----|----
--force, -f|이미지를 강제로 삭제
--no-prune|중간 이미지를 삭제하지 않음

+ `docker image prune [옵션]`
+ 사용하지 않는 Docker 이미지를 삭제
+ 옵션

옵션|설명
----|----
--all, -a|사용하지 않은 이미지를 모두 삭제
--force, -f|이미지를 강제로 삭제

#####8. Docker Hub에 로그인(docker lgoin)
+ `docker login [옵션] [서버]`
+ 옵션

옵션|설명
---|--
--password, -p | 비밀번호
--username, -u| 사용자명
+ 옵션을 지정하지 않으면 사용자명과 비밀번호를 물어봄

#####9. 이미지 업로드(docker image push)
+ `docker image push 이미지명[:태그명]`
+ `<Docker Hub 사용자명>/이미지명[:태그명]`

#####10. Docker Hub에서 로그아웃(docker logout)
+ `docker logout [서버명]`

# 
###4.2 Docker 컨테이너 생성/시작/정지
#####1. Docker 컨테이너의 라이프 사이클
+ 컨테이너 생성(docker container create 명령)
	+ 이미지로부터 컨테이너를 생성
	+ 이미지의 실체는 'Docker에서 서버 기능을 작동시키기 위해 필요한 디렉토리 및 파일들
	+ Linux의 작동에 필요한 /etc나 /bin 등과 같은 디렉토리 및 파일들
	+ 명령을 실행하면 이미지에 포함될 Linux의 디렉토리와 파일들의 스냅샷을 취함
+ 컨테이너 생성 및 시작(docker container run 명령)
	+ 컨테이너를 작성하기만 할 뿐  컨테이너를 시작하지는 않음 -> 컨테이너를 시작할 준비가 된 상태
	+ 이미지로부터 컨테이너를 생성하고, 컨테이너 상에서 임의의 프로세스를 시작
+ 컨테이너 시작(docker container start 명령)
	+ 정지 중인 컨테이너를 시작할 때 사용
+ 컨테이너 정지(docker container stop 명령)
	+ 실행 중인 컨테이너를 정지시킬 때 사용
+ 컨테이너 삭제(docker container rm 명령)
	+ 컨테이너를 삭제할 때 사용
+ 그 외
	+ 컨테이너의 상태 확인 : `docker container ps`
	+ 컨테이너 일시정지 : `docker container pause`

#####2. 컨테이너 생성 및 시작(docker container run)
+ `docker container run [옵션] 이미지명[:태그명] [인수]`
+ 옵션

옵션|설명
---|---
--attach, -a|표준 입력(STDIN), 표준 출력(STDOUT), 표준 오류 출력(STDERR)에 어태치한다.
--cidfile|컨테이너 ID를 파일로 출력한다
--detach, -d|컨테이너를 생성하고 백그라운드에서 실행한다.
--interactive, -I | 컨테이너의 표준 입력을 연다.
--tty, -t|단말기 디바이스를 사용한다.

+ docker container run 대화식 실행
`docker container run -it --name "test1" centos /bin/cal`
	+ docker container run : 컨테이너를 생성 및 실행
	+ -it : 콘솔에 결과를 출력하는 옵션
	+ --name "test1" : 컨테이너 명
	+ centos : 이미지명
	+ /bin/cal : 컨테이너에서 실행할 명령

#####3. 컨테이너의 백그라운드 실행(docker container run)
+ `docker container run [실행 옵션] 이미지명[:태그명] [인수]`
+ 옵션

옵션|설명
----|----
--detach, -d | 백그라운드에서 실행
--user, -u | 사용자명을 지정
--restart=[no &#124; on-failure &#124; on-failure:횟수n &#124; always &#124; unless-stopped] | 명령의 실행 결과에 따라 재시작을 하는 옵션
--rm | 명령 실행 완료 후에 컨테이너를 자동으로 삭제

+ docker container run의 백그라운드 실행
`docker container run -d centos /bin/ping localhost`
	+ docker container run : 컨테이너를 생성 및 실행
	+ -d : 백그라운드에서 실행하는 옵션
	+ centos : 이미지명
	+ /bin/ping localhost : 컨테이너에서 실행할 명령

+ --restart 옵션

설정값|설명
-----|----
no | 재시작하지 않는다.
on-failure | 종료 스테이터스가 0이 아닐 때 재시작한다.
on-failure:횟수 n|종료 스테이터스가 0이 아닐 때 n번 재시작한다.
always|항상 재시작한다.
unless-stopped | 최근 컨테이너가 정지 상태가 아니라면 항상 재시작한다.

#####4. 컨테이너의 네트워크 설정(docker container run)
+` docker container run [네트워크 옵션] 이미지명[:태그명] [인수]`
+ 옵션

옵션 | 설명
----|----
--add-host=[호스트명:IP 주소]|컨테이너의 /etc/hosts에 호스트명과 IP주소를 정의
--dns=[IP 주소]|컨테이너용 DNS 서버의 IP 주소 지정
--expose | 지정한 범위의 포트 번호를 할당
--mac-address=[MAC 주소] | 컨테이너의 MAC 주소를 지정
--net=[birdge&#124;none&#124;container:&lt;name &#124; id>&#124; host&#124; NETWORK]|컨테이너의 네트워크를 지정
--hostname, -h | 컨테이너 자신의 호스트명을 지정
--publish, -p[호스트의 포트 번호]:[컨테이너의 포트 번호]|호스트와 컨테이너의 포트 매핑
--publish-all, -P | 호스트의 임의의 포트를 컨테이너에 할당

+ --net 옵션의 지정

설정값 | 설명
---|---
bridge | 브리지 연결(기본값)을 사용한다
none | 네트워크에 연결하지 않는다.
container:[name &#124; id ]|다른 컨테이너의 네트워크를 사용한다.
host|컨테이너가 호스트 OS의 네트워크를 사용한다.
NETWORK | 사용자 정의 네트워크를 사용한다.

#####5. 자원을 지정하여 컨테이너 생성 및 실행(docker container run)
+ `docker container run [자원 옵션] 이미지명[:태그명] [인수]`
+ 옵션

옵션|설명
--|--
--cpu-shares, -c|CPU의 사용 배분(비율)
--memory, -m|사용할 메모리를 제한하여 실행(단위는 b, k, m, g 중 하나)
--volume=[호스트의 디렉토리]:[컨테이너의 디렉토리], -v | 호스트와 컨테이너의 디렉토리를 공유

#####6. 컨테이너를 생성 및 시작하는 환경을 지정(docker container run)
+ `docker container run [환셩설정 옵션] 이미지명[:태그명] 인수`
+ 옵션

옵션|설명
--|--
--env=[환경변수], -e|환경변수를 설정한다.
--env-file=[파일명]|환경변수를 파일로부터 설정한다.
--read-only=[true &#124; false]|컨테이너의 파일 시스템을 읽기 전용으로 만든다.
--workdir=[패스], -w | 컨테이너의 작업 디렉토리를 지정한다.
--user=[사용자명], -u | 사용자명 또는 UID를 지정한다.

#####7. 가동 컨테이너 목록 표시(docker container ls)
+ `docker container ls [옵션]`
+ 옵션

옵션|설명
----|----
--all, -a| 실행 중/ 정지 중인 것도 포함하여 모든 컨테이너를 표시
--filter, -f|표시할 컨테이너의 필터링
--format| 표시 포맷을 지정
--last, -n|마지막으로 실행된 n건의 컨테이너만 표시
--latest, -l | 마지막으로 실행된 컨테이너만 표시
--no-trunc | 정보를 생략하지 않고 표시
--quiet, -q|컨테이너 ID만 표시
--size, -s|파일 크기 표시

+ docker container ls 명령 결과

항목|설명
--|--
CONTAINER ID|컨테이너 ID
IMAGE|컨테이너의 바탕이 된 이미지
COMMAND|컨테이너 안에서 실행되고 있는 명령
CREATED|컨테이너 작성 후 경과 시간
STATUS|컨테이너의 상태(restarting &#124; running &#124; paused &#124; exited)
PORTS|할당된 포트
NAMES|컨테이너 이름

+ --format 출력 형식의 지정

플레이스 홀더|설명
--|--
.ID|컨테이너 ID
.Image|이미지 ID
.Command|실행 명령
.CreatedAt|컨테이너가 작성된 시간
.RunningFor|컨테이너의 가동 시간
.Ports|공개 포트
.Status|컨테이너 상태
.Size|컨테이너 디스크 크기
.Names|컨테이너명
.Mounts|볼륨 마운트
.Networks|네트워크명

#####8. 컨테이너 가동 확인(docker container stats)
+ `docker container stats [컨테이너 식별자]`
+ 결과

항목|설명
---|---
CONTAINER ID|컨테이너 식별자
NAME|컨테이너명
CPU %|CPU 사용률
MEM USAGE/LIMIT|메모리 사용량/컨테이너에서 사용할 수 있는 메모리 제한
MEM %|메모리 사용률
NET I/O|네트워크 I/O
BLOCK I/O|블록 I/O
PIDS|PID(Windows 컨테이너 제외)

#####9. 컨테이너 시작(docker container start)
+ `docker container start [옵션] <컨테이너 식별자> [컨테이너 식별자]`
+ 옵션

옵션|설명
---|---
--attach, -a|표준 출력, 표준 오류 출력을 연다.
--interactive, -I|컨테이너의 표준 입력을 연다.

#####10. 컨테이너 정지(docker container stop)
+ `docker container stop [옵션] <컨테이너 식별자> [컨테이너 식별자]`
+ 옵션

옵션|설명
--|--
--time, -t|컨테이너의 정지 시간을 지정(기본값은 10초)

#####11. 컨테이너 재시작(docker container restart)
+`docker container restart [옵션] <컨테이너 식별자> [컨테이너 식별자]`
+ 옵션

옵션|설명
--|--
--time, -t|컨테이너의 재시작 시간을 지정(기본값은 10초)

#####12. 컨테이너 삭제(docker container rm)
+ `docker container rm [옵션] <컨테이너 식별자> [컨테이너 식별자]`
+ 옵션

옵션 | 설명
--|--
--force, -f|실행 중인 컨테이너를 강제로 삭제
--volumes, -v | 할당한 볼륨을 삭제

#####13. 컨테이너 중단/재개(docker container pause/docker container unpause)
+ `docker container pause <컨테이너 식별자>`

+ 중단 컨테이너의 재개 : `docker container unpause webserver`

# 
###4.3 Docker 컨테이너 네트워크
#####1. 네트워크 목록 표시(docker  network ls)
+ `docker network ls [옵션]`
+ 옵션

옵션|설명
--|--
--filter = [ ], -f | 출력을 필터링한다.
--no-trunc|상세 정보를 출력한다.
--quiet, -q | 네트워크 ID만 표시한다.

+ 필터링에서 이용할 수 있는 키

값|설명
--|--
driver|드라이버 지정
id|네트워크 ID
label | 네트워크에 설정된 라벨(label=&lt;key> 또는 label=&lt;key>=&lt;value>로 지정한다.)
name|네트워크명
scope|네트워크의 스코프(swarm/global/local)
type|네트워크의 타입(사용자 정의 네트워크 custom/정의 완료 네트워크 builtin)

#####2. 네트워크 작성(docker network create)
+ `docker network create [옵션] 네트워크`
+ 옵션

옵션|설명
--|--
--driver, -d | 네트워크 브리지 또는 오버레이(기본값은 bridge)
--ip-range|컨테이너에 할당하는 IP 주소의 범위를 지정
--subnet|서브넷을 CIDR 형식으로 지정
--ipv6| IPv6 네트워크를 유효화할지 말지(true/false)
-label | 네트워크에 설정하는 라벨

#####3. 네트워크 연결(docker network connect/docker network disconnect)
+ `docker network connect [옵션] 네트워크 컨테이너`
+ 옵션

옵션|설명
--|--
--ip|IPv4 주소
--ip6|IPv6 주소
--alias | 앨리어스명
--link|다른 컨테이너에 대한 링크

+ 네트워크에 대한 연결 해제 : `docker network disconnect <네트워크명> <컨테이너명>`

#####4. 네트워크 상세 정보 확인(docker network insepct)
+ `docker network insepect [옵션] 네트워크`

#####5. 네트워크 삭제(docker network rm)
+ `docker network rm [옵션] 네트워크`

# 
###4.4 가동 중인 Docker 컨테이너 조작
#####1. 가동 컨테이너 연결(docker container attach)
+ `docker container attach <컨테이너명>`
+ 연결된 컨테이너를 종료 : Ctrl + C
+ 컨테이너에서 분리 : Ctrl + P, Ctrl + Q

#####2. 가동 컨테이너에서 프로세스 실행(docker container exec)
+ `docker container exec [옵션] <컨테이너 식별자> <실행할 명령> [인수]
+ 옵션

옵션|설명
--|--
--detach, -d| 명령을 백그라운드에서 실행한다.
--interactive, -i| 컨테이너의 표준 입력을 연다.
--tty, -t | tty(단말 디바이스)를 사용한다.
--user, -u|사용자명을 지정한다.

+ exec 명령은 실행 중인 컨테이너에서만 실행 가능

#####3. 가동 컨테이너의 프로세스 확인(docker container top)
+ `docker container top <컨테이너명>`

#####4. 가동 컨테이너의 포트 전송 확인(docker container port)
+ `docker container port <컨테이너명>`

#####5. 컨테이너의 이름 변경(docker container rename)
+ `docker container rename <컨테이너명> <변경할 컨테이너명>`

#####6. 컨테이너 안의 파일을 복사(docker container cp)
+ `docker container cp <컨테이너 식별자:<컨테이너 안의 파일 경로> <호스트의 디렉토리 경로>`
+ `docker container cp <호스트의 파일> <컨테이너 식별자>:<컨테이너 안의 파일 경로>

#####7. 컨테이너 조작의 차분 확인(docker container diff)
+ `docker container diff <컨테이너 식별자>`
+ 변경의 구분

구분|설명
--|--
A|파일 추가
D|파일 삭제
C|파일 수정

# 
###4.5 Docker 이미지 생성
#####1. 컨테이너로부터 이미지 작성(docker container commit)
+ `docker container commit [옵션] <컨테이너 식별자> [이미지 [:태그명]]
+ 옵션

옵션|설명
--|--
--auther, -a | 작성자를 지정한다.
--message, -m | 메시지를 지정한다.
--change, -c | 커미트 시 Dockerfile 명령을 지정한다.
--pause, -p| 컨테이너를 일시 정지하고 커미트한다.

#####2. 컨테이너를 tar 파일로 출력(docker container export)
+ `docker container export <컨테이너 식별자>`

#####3. tar 파일로부터 이미지 작성(docker image improt)
+ `docker image import <파일 또는 URL> | - [이미지명 [:태그명]]`
+ image import 명령으로 지정할 수 있는 아카이브 파일 : tar, tar.gz, tgz, bzip, tar.xz, txz

#####4. 이미지 저장(docker image save)
+ `docker image save [옵션] <저장 파일명> [이미지명]
+ 저장할 파일명은 -o 옵션으로 저장

#####5. 이미지 읽어 들이기(docker image load)
+ `docker image load [옵션]`
+ 읽어 들일 파일명은 -i 옵션으로 지정

#####6. 불필요한 이미지/컨테이너를 일괄 삭제(docker system prune)
+ `docker system prune [옵션]`
+ 옵션

옵션|설명
--|--
--all, -a|사용하지 않는 리소스를 모두 삭제한다.
--force, -f|강제적으로 삭제한다.


