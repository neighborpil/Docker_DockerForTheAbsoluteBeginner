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
   + -e **환경변수** : 환경변수를 지정하는 것이 가능하다(export 변수명=값), 설정된 변수는 docker **insptect** 컨테이너명으로 확인 가능
   + --link **host컨테이너명**:**내부 지칭명**(Deprecated) : DB와 같이 다른 컨테이너를 연결하여 사용한다
   + --cpus=[소수점] : 사용하는 CPU의 사용량을 제한한다
   + --memory=[용량단위] : 사용하는 메모리의 용량을 제한한다(ex: --memory=[100m], --memory=[1g] 
```
docker run -v /opt/datadir:/var/lib/mysql mysql
docker run -e APP_COLOR=green simple-webapp-color
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
sudo lsof -i 프로토콜명(TCP, UDP..):포트명

sudo kill -15 PID
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
   + \# docker rm zz0
 - 컨테이너 ID는 여러개를 한꺼번에 지울 수 있다
   + \# docker rm zz0 e30
   
 ### ※ 도커 컨테이너 일괄삭제
 ```
 # docker rm $(docker ps -a -q)
 ```


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
 
# [나만의 이미지 만들기]

## 순서
 1. OS - Ubuntu
 2. Update apt repo
 3. install dependencies using apt
 4. install python dependencies using PIP
 5. Copy source code to /apt folder
 6. Run the web server using "flast" command
 
```
FROM Ubuntu
RUN apt-get update && apt-get -y install python
```

## Code Exmaple
1. 도커 생성 후 웹서버를 생성한다
```
# docker run -it ubuntu bash
------Inside ubuntu container
# apt-get update
# apt-get install -y pyton3
# python3
>>> exit()
# apt-get install -y python3-pip
# pip3 install flask
# vim /opt/app.py
---------------------
import os
from flask import Flask
app = Flask(__name__)
@app.route("/")
def main():
    return "welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)
-------------------------------
# cd /opt
# FLASK_APP=app.py flask run --host=0.0.0.0
```
이후 웹브라우저로 172.17.0.2:5000으로 접속하여 확인

2. 생성 순서를 기록한다<br>
2.1. apt-get update<br>
2.2. apt-get install -y python3<br>
2.3. apt-get install python3-pip<br>
2.4. pip3 install flask<br>
2.5. Create/Copy application code to /opt/app.py<br>
2.6 FLASK_APP=/opt/app.py flask run --host=0.0.0.0<br>

3. 폴더 생성 및 옮기기
```
# mkdmir my-simple-webapp
# cd my-simple-webapp
# cat > Dockerfile

FROM ubuntu

Run apt-get update
RUN apt-get install -y python3 python3-pip
RUN pip3 install flask

COPY app.py /opt/app.py

ENTRYPOINT cd /opt && FLASk_APP=/opt/app.py flask run --host=0.0.0.0
    
-- Ctrl + C로 파일 작성 종료

# cat > app.py

import os
from flask import Flask
app = Flask(__name__)

@app.route("/")
def main():
    return "welcome!"

@app.route('/how are you')
def hello():
    return 'I am good, how about you?'

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=8080)

-- Ctrl + C로 파일 작성 종료

```

4. 빌드

```
# docker build .
# docker build . -t neighborpil/my-simple-webapp
```

5. 이미지 확인

\# docker images

6. repository에 푸시하기
 - 먼저 로그인이 되어 있어야 한다
   + \# docker login
   + 만약 없다면 https://hub.docker.com에서 생성해야 한다
 
 - 이미지를 빌드한다
   + 빋드할 때에 반드시 name을 입력해야 한다
   + \# docker build . -t **neighborpil**/my-simple-webapp
 - 이미지를 푸시한다
   + docker push **계정명**/**이미지명**

 - 웹브라우저로 hug.docker.com에 로그인하여 생성된 리파지토리 확인한다.

## ENTRYPOINT AND CMD
 - ENTRYPOINT : 도커파일에서 실행할 프로그램
   + 다시 입력받는 것 불가능
 - CMD : 도커파일에서 실행될 명령어
   + Docker run 커맨드로 도커 실행시 다시 입력이 가능하다

# [DOCKER COMPOSE]
 - 여러개의 도커 컨테이너를 묶어서 실행하는 것
 - yaml 설정파일을 설정하고 추후에 **\# docker-compose up** 명령어로 실행
 - Docker-compose.yml
   + yaml 포맷 파일
   + 도커 설정파일
 - Version2이후에는 yaml 파일 내에 **Version: 버전**을 명시해줘야 함
## 버전별 차이점
 - Version 1
   + bridged네트워크만 사용
   + link로 다른 컨테이너를 연결해줘야함
 - Version 2 

## 도커 Compose 예제

```
apt install git

mkdir sample-application
cd sample-application
git clone https://github.com/neighborpil/example-voting-app.git
cd example-voting-app
cd vote
docker build . -t voting-app
docker run -d --name=redis redis
docker run -d -p 5000:80 --link redis:redis voting-app
docker run -d --name=db -e POSTGRES_PASSWORD=postgres postgres:9.4
cd ..
cd worker
cat Dockerfile
docker build . -t worker-app
docker run -d --link redis:redis --link db:db worker-app
cd ..
cd result
ls -l
cat Dockerfile
docker build . -t result-app
docker run -d -p 5001:80 --link db:db result-app
```
이후 127.0.0.1:5000에서 투표하고 127.0.0.1:5001에서 결과 확인 가능

-----------------------------
# [Docker Compose]

## 설치방법
 1. 설치 페이지에서 설치 방법 확인
```
https://docs.docker.com/compose/install/
```
 2. 설치파일 다운로드 url 

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
 3. 권한 부여
```
sudo chmod +x /usr/local/bin/docker-compose
```
 4. 실행중인 컨테이너가 있다면 종료
```
docker stop $(docker ps -q)
```
 5. docker-compse 파일 제작
```
cat > docker-compose.yml
redis:

vi docker-compose.yml
redis:
  image: redis

db:
  image: postgres:9.4
  environment:
    - POSTGRES_PASSWORD=postgres

vote:
  image: voting-app
  ports:
    - 5000:80
  links:
    - redis

worker:
  image: worker-app
  links:
    - db
    - redis

result:
  image: result-app
  ports:
    - 5001:80
  links:
    - db

:wq

```

 6. 도커 컴포즈 시작
```
docker-compose up
```


## Compose File References
 - 버전확인 : https://docs.docker.com/compose/compose-file/

## Docker Compose Version "3"
 - 상단에 버전 명시 필요(version: "3")
 - services:이하에 실제 내용 작성
 - 내부 네트워크를 사용하기 때문에 link없어도 된다

```
version: "3"
services:

  redis:
    image: redis

  db:
    image: postgres:9.4
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres

  vote:
    image: voting-app
    ports:
      - 5000:80

  worker:
    image: worker-app

  result:
    image: result-app
    ports:
      - 5001:80

```
#### ※ 3버전 좀더 디테일하게
```
version: '3'
services:
  redis:
    image: redis
    networks:
      - back-end
    volumes:
      - redis-data:/var/lib/redis
  db:
    image: postgres:9.4
    networks:
        - back-end
    volumes:
      - db-data:/var/lib/postgresql/data

  vote:
    image: voting-app
    ports:
      - "5000:80"
    networks:
        - back-end
        - front-end

  result:
    image: result-app
    ports:
        - 5001:80
    networks:
        - back-end
        - front-end

  worker:
    image: worker-app
    networks:
        - back-end

networks:
  front-end:
    driver: bridge
  back-end:
    driver: bridge

volumes:
  redis-data:
  db-data:
```


# [Docker Registry]
 - 이미지는 기본적으로 **유저계정/이미지명** 으로 구성된다
 - 기본적으로 이미지는 앞에 docker.io라는 레지스트리가 생략된 상태이다.
```
docker.io/nginx/nginx
```
 - docker.io는 public 레지스트리로, 프라이빗 레지스트리 사용도 가능하다.
 - private registry를 사용할 경우 pull 또는 push 할 때에 로그인을 해야한다
 - 유명한 private registry에는 azure, aws등이 있다
 - 사용방법
   1. 로그인을 실시한다
```
docker login private-registry.io
```

   3. 이미지를 실행한다
```
docker run private-registry.io/apps/internal-app
```

## private registry를 사용하지 않고 실행중인 이미지를 배포하는 방법
  - docker는 자체로 registry의 기능을 한다

1. 이미지를 실행한다
```
docker run -d -p 5000:5000 --name registry registry:2
```
2. docker image tag를 써서 이미지를 생성한다
```
docker image tag my-image localhost:5000/my-image
```
3. 이미지를 push한다
```
docker push localhost:5000/my-image
```
4. 이미지를 pull한다
```
docker pull localhost:5000/my-image
```
5. 원격지에서 이미지를 pull한다
```
docker pull 192.168.56.100:5000/my-image
```

----------------
# [Docker Engine]
 - 도커는 3부분으로 구성되어 있다
   + Docker CLI : 사용자의 명령어를 입력하는 부분
   + REST API : 사용자의 명령어를 받아들이는 부분
   + Docker Deamon : 도커의 명령어를 처리하는 부분
 - Docker CLI는 원격에서 실행 가능하다

## 도커가 virtual 시스템이면서 host운영체제의 자원을 모두 운영가능한 이유
 - 리눅수의 PID시스템을 이용하여서 사용 가능하다
 - 리눅스는 PID1이 실행되고 다른 모든 child 프로세스를 실행시킨다
 - 도커는 가상 머신을 실행시킬 때 리눅스의 PID를 부여하고, 내부적으로 가상 PID를 1부터 다시 부여해 사용한다

도커 PID 확인(도커 내에서는 PID1이 운영체제에서 다르게 부여되어 있다
```
docker exec 922fc85fb203 ps -eaf

ps -eaf | grep /usr/local/openjdk-11/bin
```


## 도커 명령어 실행[exec]
 - 도커 커멘드를 실행한다

## docker exec [컨테이너ID] ps -eaf
 - 현재 컨테이너에서 실행중인 모든 프로세스를 표시한다

----------------
# [Docker Storage]
 - 도커를 설치하면 /var/lib/docker 폴더가 생성되고 그 아래에 나머지 프로그램들이 설치된다
 - 도커는 명령어를 한 라인씩 실행하면 각각의 레이어를 만들고 변경사항만을 기록한다
 - 도커의 이미지에서 생성 또는 수정한 파일은 컨테이너가 종료되면 사라진다
 - 파일을 보존하고 싶다면 read/write layer를 설정해야한다
   + **볼륨마운팅**: docker volumn create data_volumn:/var/lib/mysql mysql
   + 위와 같이 하여 볼륨을 생성한다
   + docker run -v data_volumn:/var/lib/mysql mysql
   + 위와 같이 실행하면 /var/lib/mysql 폴더내의 모든 파일들은 호스트 운영체제의 /var/lib/docker/volumns/data_volumn에 저장이 된다
   + **바인드마운팅**: 만약 외부의 저장소에 저장하고 싶다면 -v옵션을 아래와 같이 하면 된다
   + docker run -v /data/mysql:/var/lib/mysql mysql
   + -v 옵션을 사용하는 것은 옛날 방식이고 요즘에는 **--mount**옵션을 사용한다
```
docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
```

### 도커 설치정보 확인
 - docker info
```
docker info
```

### 도커 이미지 히스토리 확인
 - docker history 이미지명:버전
```
docker history tomcat:latest
```

## 도커 이미지 생성 테스트
 - 도커파일을 만들어 빌드한 후 저장되는곳 확인
 - 한 줄이 실행될 때마다 레이어가 생성되고 레이어에 기록된다
 - 따라서 다시 빌드할 때에 각 레이어에 대한 캐쉬를 가지고 빌드하기 때문에 이전과정은 생략이 가능하다
 1. 도커파일 생성
```
docker build .
```
 2. 도커파일 이름 변경
```
docker build . -t simple-webapp
```

## 도커 스토리지
 - docker info 명령어를 통하여 자기가 어떤 스토리지 타입인지 확인 가능
### 드라이별 Default storage drivers
 - Ubuntu: All 

#### ※현재 디렉토리내 파일 용량 구하기
```
#du -sh *
```

### 도커 시스템에서 사용하는 전체 용량 확인
 - 옵션
   + -v 각각 이미지들마다 상세 정보를 보여줌
```
#docker system df -v
```


#### ※ mysql 비밀번호 초기 설정하기
$ docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql


## Docker Network
### 도커네트워크의 종류
 1. Bridge
```
$docker run unbunto
```
  - 172.17.0.xxx
  - 기본적으로 하나의 브릿지 네트워크가 존재
  - 하지만 추가 할 수 있다
 ```
 docker network create \
  -- driver bridge \
  -- subnet 182.18.0.0/16
  custom-isolated-network
 
 ```

 2. none
  - 연결없음
 ```
 $docker run Ubuntu --network=none
 ```
 4. host
  - 호스트의 컨테이너와 동기화가 된다. 하나만 사용가능
 ```
 $docker run Ubuntu --network=host
 ```

### 도커 네트워크 검색
```
$docker network ls
```
### 컨테이너의 네트워크를 확인하는 방법
```
$docker inspect container_name
```

### 도커 네트워크 서브넷 확인
```
$ docker network inspect bridge
$ docker network inspect wp-mysql-network
```

### 도커 서브넷 생성하기
```
$docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network

```
#### ※ mysql 5.6, 초기비밀번호 db_pass123, 이름은 mysql-db, 네트워크는 wp-mysql-network 사용
```
docker run -d -e MYSQL_ROOT_PASSWORD=db_pass123 --name mysql-db --network wp-mysql-network mysql:5.6
```
#### 포트외부38080, 내부8080, 네트워크:wp-mysql-network, db호스트: mysql-db, db암호: db_pass123
```
docker run -d --name webapp --network=wp-mysql-network  -e DB_Host=mysql-db -e DB_Password=db_pass123 -p 38080:8080 --link mysql-db:mysql-db  kodekloud/simple-webapp-mysql
```


#### 도커 로그 확인
```
$ docker logs -f jenkins

```



### Docker-compose 마리아DB 세팅
 - docker-compose.yml
 - 마리아 DB 버전 10.1.48
 - passwordreset.sql파일이 동일 폴더에 있어야함
 - 외부 포트 3010
 - 비밀번호 myrootpassword
```
version: '3.7'
services:
  db-host:
    container_name: db-host
    image: mariadb:10.1.48
    restart: always
    command: --init-file=/passwordreset.sql
    ports:
      - "3310:3306"
    environment:
      - TZ=Asia/Seoul
      - MYSQL_ROOT_PASSWORD=myrootpassword
    volumes:
      - "$PWD/db_data:/var/lib/mysql"
      - "$PWD/passwordreset.sql:/passwordreset.sql:z"
    networks:
      - net
networks:
  net:
```
 - 비밀번호 초기화 파일
 - passwordreset.sql
```
CREATE USER IF NOT EXISTS root@localhost IDENTIFIED BY 'myrootpassword';
SET PASSWORD FOR root@localhost = PASSWORD('myrootpassword');
GRANT ALL ON *.* TO root@localhost WITH GRANT OPTION;

CREATE USER IF NOT EXISTS root@'%' IDENTIFIED BY 'myrootpassword';
SET PASSWORD FOR root@'%' = PASSWORD('myrootpassword');
GRANT ALL ON *.* TO root@'%' WITH GRANT OPTION;

CREATE USER IF NOT EXISTS myid@'%' IDENTIFIED BY 'mypassword';
SET PASSWORD FOR myid@'%' = PASSWORD('mypassword');
GRANT ALL ON *.* TO myid@'%' WITH GRANT OPTION;

```


### Docker-compose 톰캣 & 마리아DB 세팅
 - docker-compose.yml
```
version: '3.7'
services:
  roman2023_db:
    container_name: roman2023_db
    image: mariadb:10.1.48
    restart: always
    command: --init-file=/passwordreset.sql
    ports:
      - "3310:3306"
    environment:
      - TZ=Asia/Seoul
      - MYSQL_ROOT_PASSWORD=1234
    volumes:
      - "$PWD/mariadb/db_data:/var/lib/mysql"
      - "$PWD/mariadb/passwordreset.sql:/passwordreset.sql:z"
    networks:
      - net
  roamn2023_tomcat:
    container_name: roman2023_tomcat
    image: tomcat:8.0.53-jre8
    build:
      context: $PWD/tomcat/.
      dockerfile: Dockerfile
    depends_on:
      - roman2023_db
    ports:
      - "8810:8080"
      - "10022:22"
    volumes:
      - "$PWD/tomcat/webapps:/usr/local/tomcat/webapps"
      - "$PWD/tomcat/logs:/usr/local/tomcat/logs"
    networks:
      - net
networks:
  net:
```

 - mariadb/passwordreset.sql
```
CREATE USER IF NOT EXISTS root@localhost IDENTIFIED BY '1234';
SET PASSWORD FOR root@localhost = PASSWORD('루트비밀번호');
GRANT ALL ON *.* TO root@localhost WITH GRANT OPTION;

CREATE USER IF NOT EXISTS root@'%' IDENTIFIED BY '1234';
SET PASSWORD FOR root@'%' = PASSWORD('루트비밀번호');
GRANT ALL ON *.* TO root@'%' WITH GRANT OPTION;

CREATE USER IF NOT EXISTS bluecom@'%' IDENTIFIED BY '1234';
SET PASSWORD FOR bluecom@'%' = PASSWORD('비밀번호');
GRANT ALL ON *.* TO bluecom@'%' WITH GRANT OPTION;
```

 - tomcat/Dockerfile
 - 원래 톰캣 이미지가 shutdown되면 바로 꺼진다. 안꺼지게 하기 위해 entrypoint에 tail 붙여줌
 - 대신 자동으로 시작되지 않는다.
    + 완료 후 "docker exec -it roman2023_tomcat bash로 들어가서
    + /usr/local/tomcat/bin/startup.sh 해줘야 실행된다.
```
FROM tomcat:8.0.53-jre8

RUN apt-get update

RUN apt-get -y upgrade

RUN apt-get install -y openssh-server

RUN echo "root:루트비밀번호" | chpasswd

ENTRYPOINT service ssh restart && tail -F /usr/local/tomcat/logs/catalina.out

```


### centos7 with systemd
```


FROM centos:centos7.9.2009

ENV container docker

RUN yum -y install systemd; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]

CMD ["/usr/sbin/init"]

```
--------------------------------------
### 마리아 DB 구동 스크립트
 - 버전 10.4
 - root 비밀번호: adminpassword
 - mariaStart.sh
 - volume: db_data
 - 외부포트 3306
```
echo start mariadb 10.4
echo --------------------
docker run --name mariadb10.4 \
        -e MARIADB_ROOT_PASSWORD=adminpassword \
        -d \
        --restart=always \
        -p 3306:3306 \
        -v $PWD/db_data:/var/lib/mysql \
        mariadb:10.4
```
