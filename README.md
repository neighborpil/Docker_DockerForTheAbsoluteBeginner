# Docker_DockerForTheAbsoluteBeginner
Hands On Codes for practicing

--------------------
#API Document
http://docs.docker.com

# 도커 연습 랩
https://kodekloud.com/courses/911976/lectures/16792271


-----------------------------
# How to insall docker on ubuntu
https://docs.docker.com/engine/install/ubuntu/



### ※Ubuntu Version Check Command
```
cat /etc/issue
```

# [도커 인스톨 방법]
 1. 도커 설치 스크립트 다운로드
```
$ curl -fsSL https://get.docker.com -o get-docker.sh
```
 2. 스크립트 실행
```
$ sudo sh get-docker.sh
```
 3. 설치 완료후 도커 버전 확인
```
$ sudo docker version
```

### ※ systemctl status 서비스명
 - 프로세스가 동작중인지 확인

###※ systemctl start 서비스명
 - 프로세스 시작

## wsl 2버전에서 도커 시작방법
 - wsl2에서는 systemd가 없어 systemctl을 사용 할 수 없다.
 - 도커를 실행하려면 아래 방식으로 프로세스 시작이 가능하다
   sudo /etc/init.d/docker start
 

# [도커 이미지 사이트]
 - https://hub.docker.com

# [도커 커맨드]

## docker run [옵션] (**이미지명**)[:버전] [커맨드]
 - 도커 실행방법
   + whalesay 는 도커 튜토리얼을 위한 이미지이다(https://hub.docker.com/search?q=whalesay&type=image)
```
$ sudo docker run docker/whalesay cowsay Hello-World!
```
   + 만약 로컬에 이미지가 없다면 도커가 자동으로 해당 다운로드 한 후에 컨테이너를 실행한다
 - 옵션
   + -d : backgrund에서 동작(detached모드의 약자)
   + --name [컨테이너 이름] : 컨테이너의 이름을 지정
   + -p **외부포트**:**내부포트** : 외부 포트와 내부 포트를 연결해준다(도커 인터넷 실행 예제 이미지: kodekloud/simple-app)
   + -v **외부경로**:**내부경로** : 컨테이너에서 발생하는 데이터를 외부경로에 저장한다
   + -u **사용자명** : 도커 실행을 위한 사용자를 지정한다
```
docker run -v /opt/datadir:/var/lib/mysql mysql
```
```
# cd
# mkdir my-jenkins-datas
# docker run -p 8080:8080 -p 50000:50000 -v /root/my-jenkins-datas:/var/jenkins_home -u root jenkins/jenkins:lts
```
   
 - 버전
   + 여러가지 이미지 버전이 있을 경우 버전을 특정할 수 있다. 만약 특정하지 않으면 latest가 설치됨
   + 버전의 docker images 커맨드를 실행했을 경우의 태그에 해당한다
   + hub.docker.com에서 이미지를 검색해보면 사용 가능한 버전이 나온다
 - 커맨드
   + sleep 숫자 : 해당하는 숫자의 초만큼 슬립 상태로 실행된다

### ※ ubuntu에서 IP 확인하기
```
$ hostname -I 
```

### ※ ubuntu에서 사용중인 포트 확인 후 삭제하기
```
sudo lsof -i **프로토콜명(TCP, UDP..)**:**포트명**

sudo kill -15 **PID**
```


### docker run -it (centos) bash
 - 도커를 시작하고 안의 컨테이너에 배쉬로 연결
 - 도커내 배쉬에서 빠져나올 때는 **exit** 를 치면 된다
 - i는 input을 의미하고, t는 terminal을 의미한다

## docker ps -옵션
 - 현재 실행중인 컨테이너의 정보를 보여준다
 - 옵션
   + a: 현재 실행중이거나 이전에 실행했던 모든 컨테이너의 정보를 보여준다
   + q: 프로세스 아이디만 보여준다

## docker stop (컨테이너NAME)
 - 현재 실행중인 컨테이너를 종료한다
 - 컨테이너 네임은 **docker ps** 커맨드를 했을 때 Names에 나온다
 - 동작 중인 docker를 stop command에 의해 종료하게 되면, 종료 코드가 (137)로 표시된다(docker ps 메시지에서 Exited(코드)에서 확인 가능)

## docker rm (컨테이너 ID, 컨테이너 NAME)
 - 현재 실행중인 컨테이너를 삭제한다
 - 컨테이너 ID는 **docker ps** 커맨드를 했을 때 제일 앞 CONTAINER ID, 제일 뒤 CONTAINER NAMES에서 확인 가능하다
 - 컨테이너 ID는 앞자리 몇개만 있어도 삭제 가능하다
   + $ docker rm zz0
 - 컨테이너 ID는 여러개를 한꺼번에 지울 수 있다
   + $ docker rm zz0 e30


## docker images
 - 현재 로컬에 다운 받아있는 이미지 리스트를 보여준다

## docker rmi (이미지repository)[:tag명]
 - 현재 로컬에 다운 받아있는 이미지를 삭제한다
 - 이미지를 삭제하려고 할 때에는 해당하는 이미지를 가지고 동작하는 컨테이너가 없는 것을 확인해야 한다
 - tag명
   + 없으면 latest를 삭제한다
   + 특정 버전은 반드시 입력해야 한다

 
## docker pull (이미지이름)
 - 이미지를 다운만 받는다
 - 다운받은 이미지로 컨테이너를 생성, 실행하지 않는다


## docker exec (컨테이너 ID) (명령어)
 - 컨테이너 내부의 명령어를 실행할 때에 사용한다
``` 
$ sudo docker exec 406b78f6367f cat /etc/*release*
```

## docker inspect 컨테이너 ID 또는 컨테이너 이름
 - 컨테이너의 상세 정보를 보여준다
 
## docker logs 컨테이너 ID 또는 컨테이너 이름
 -  컨테이너의 로그를 보여준다
 
## ※ 만약 도커를 -d옵션을 주지 않고 실행했을 때에 대처법
 - 이 상태에서는 Ctrl + C를 해도 종료되지 않는다
 - 다른 터미널을 열어서 거기서 docker stop으로 컨테이너를 종료한다
 
## docker attach 컨테이너 ID
 - docker run -d옵션으로 detatched되어 백그라운드에서 동작하다가, 다시 foreground에서 동작시키기 위해 사용
