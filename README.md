# Docker_DockerForTheAbsoluteBeginner
Hands On Codes for practicing

--------------------
#API Document
http://docs.docker.com

# How to insall docker on ubuntu
https://docs.docker.com/engine/install/ubuntu/

��Ubuntu Version Check Command
 - cat /etc/issue

# ��Ŀ �ν��� ���
 1. ��Ŀ ��ġ ��ũ��Ʈ �ٿ�ε�
  - $ curl -fsSL https://get.docker.com -o get-docker.sh
 2. ��ũ��Ʈ ����
  - $ sudo sh get-docker.sh
 3. ��ġ �Ϸ��� ��Ŀ ���� Ȯ��
  - $ sudo docker version

�� systemctl status ���񽺸�
 - ���μ����� ���������� Ȯ��

�� systemctl start ���񽺸�
 - ���μ��� ����

# wsl 2�������� ��Ŀ ���۹��
 - wsl2������ systemd�� ���� systemctl�� ��� �� �� ����.
 - ��Ŀ�� �����Ϸ��� �Ʒ� ������� ���μ��� ������ �����ϴ�
   sudo /etc/init.d/docker start
 

# ��Ŀ �̹��� ����Ʈ
 - https://hub.docker.com

# docker run �̹�����
 -��Ŀ ������
 - whalesay �� ��Ŀ Ʃ�丮���� ���� �̹����̴�(https://hub.docker.com/search?q=whalesay&type=image)
 - $ sudo docker run docker/whalesay cowsay Hello-World!
 - ���� ���ÿ� �̹����� ���ٸ� �ٿ�ε� �� �Ŀ� �����̳ʸ� �����Ѵ�
  

[��Ŀ Ŀ�ǵ�]
# docker ps
 - ���� �������� �����̳��� ������ �����ش�

# docker ps -a
 - ���� �������̰ų� ������ �����ߴ� ��� �����̳��� ������ �����ش�

# docker stop [�����̳�names]
 - ���� �������� �����̳ʸ� �����Ѵ�

# docker rm [�����̳�names]
 - ���� �������� �����̳ʸ� �����Ѵ�

# docker images
 - ���� ���ÿ� �ٿ� �޾��ִ� �̹��� ����Ʈ�� �����ش�

# docker rmi [�̹���repository]
 - ���� ���ÿ� �ٿ� �޾��ִ� �̹����� �����Ѵ�
 - �̹����� �����Ϸ��� �� ������ �ش��ϴ� �̹����� ������ �����ϴ� �����̳ʰ� ���� ���� Ȯ���ؾ� �Ѵ�

 
# docker pull �̹����̸�
 - �̹����� �ٿ�޴´�
 - �ٿ���� �̹����� �����̳ʸ� ����, �������� �ʴ´�

# docker run -it centos bash
 - ��Ŀ�� �����ϰ� ���� �����̳ʿ� �转�� ����
 - ��Ŀ�� �转���� �������� ���� **exit** �� ġ�� �ȴ�