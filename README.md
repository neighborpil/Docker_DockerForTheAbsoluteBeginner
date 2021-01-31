# Docker_DockerForTheAbsoluteBeginner
Hands On Codes for practicing

--------------------
#API Document
http://docs.docker.com

# How to insall docker on ubuntu
https://docs.docker.com/engine/install/ubuntu/

※Ubuntu Version Check Command
 - cat /etc/issue

# 도커 인스톨 방법
 1. 도커 설치 스크립트 다운로드
  - $ curl -fsSL https://get.docker.com -o get-docker.sh
 2. 스크립트 실행
  - $ sudo sh get-docker.sh
 3. 설치 완료후 도커 버전 확인
  - $ sudo docker version

※ systemctl status 서비스명
 - 프로세스가 동작중인지 확인

※ systemctl start 서비스명
 - 프로세스 시작

# wsl 2버전에서 도커 시작방법
 - wsl2에서는 systemd가 없어 systemctl을 사용 할 수 없다.
 - 도커를 실행하려면 아래 방식으로 프로세스 시작이 가능하다
   sudo /etc/init.d/docker start
 

# 도커 이미지 사이트
 - https://hub.docker.com

# docker run [옵션] **이미지명** [커맨드]
 - 도커 실행방법
   + whalesay 는 도커 튜토리얼을 위한 이미지이다(https://hub.docker.com/search?q=whalesay&type=image)
   + $ sudo docker run docker/whalesay cowsay Hello-World!
   + 만약 로컬에 이미지가 없다면 다운로드 한 후에 컨테이너를 실행한다
 - 옵션
   + **-d** : backgrund에서 동작
 - **커맨드**
   + sleep 숫자 : 해당하는 숫자의 초만큼 슬립 상태로 실행된다
  

[도커 커맨드]
# docker ps
 - 현재 실행중인 컨테이너의 정보를 보여준다

# docker ps -a
 - 현재 실행중이거나 이전에 실행했던 모든 컨테이너의 정보를 보여준다

# docker stop [컨테이너names]
 - 현재 실행중인 컨테이너를 종료한다

# docker rm [컨테이너names]
 - 현재 실행중인 컨테이너를 삭제한다

# docker images
 - 현재 로컬에 다운 받아있는 이미지 리스트를 보여준다

# docker rmi [이미지repository]
 - 현재 로컬에 다운 받아있는 이미지를 삭제한다
 - 이미지를 삭제하려고 할 때에는 해당하는 이미지를 가지고 동작하는 컨테이너가 없는 것을 확인해야 한다

 
# docker pull 이미지이름
 - 이미지를 다운받는다
 - 다운받은 이미지로 컨테이너를 생성, 실행하지 않는다



# docker run -it centos bash
 - 도커를 시작하고 안의 컨테이너에 배쉬로 연결
 - 도커내 배쉬에서 빠져나올 때는 **exit** 를 치면 된다
