# LAMP + pod 설치
## LAMP란?
Linux + Apache + MariaDB + Php or perl or python

### 1.	Linux 설치

-	Centos 8 설치
1)	미러사이트를 통하여 iso 파일을 다운로드
>http://isoredirect.centos.org/centos/8/isos/x86_64/

2)	vmware에 centos를 설치
 >설치 시 GUI 환경 동시에 설치하여 xwindow 환경을 같이 설치하였습니다.

### 2.	Apache 설치

1)	$ Su 명령어를 이용하여 root 계정으로 접속

2)	$ yum 명령어를 이용하여 apache 설치
>$ yum install httpd *
3)	설치 완료 후 httpd 버전 확인
>httpd -v

4)	아파치 실행
>$ service httpd start

5)	포트 확인

>$ netstat -tnlp
>Apache port Number : 80

6)	시작 프로그램 등록

>$ systemctl enable httpd

7)	방화벽 설정

>$ firewall-cmd --permanent --zone=public --add-port=80/tcp
>$ firewall-cmd –reload

8)	Apache 구동 확인

>/var/www/html 디렉토리에 index.html 파일 생성 후
“Hello World!!” 작성 후 저장
Windows 환경으로 돌아와 web browser 실행 후 ip : 80으로 접속
192.168.193.131:80
>>구동 확인.

### 3.	Maria DB 설치

1)	$ yum 명령어 이용하여 Maria DB 설치
>$ yum -y install mariadb*

2)	서비스 등록
>$ /sbin/chkconfig –level 3 mariadb on

3)	서비스 작동
>$ service mariadb start

4)	Maria DB 패스워드 설정
>$ mysqladmin -u root — password ‘sangwon’

### 4.	PHP 설치

1)	$ yum 명령어 이용하여 PHP 설치
>$ yum install php

2)	아파치 재시작
>$ service httpd restart

3)	/var/www/html 디렉토리에 index.php 파일 생성
>기존의 index.html 파일 삭제 후
Index.php 파일 생성
내용 작성
<?php
phpinfo();
?>

4)	구동 확인
>Web browser로 192.168.193.131:80 접속 확인

### 5.	Pod 설치

1)	$ yum 이용하여 podman 설치
>$ yum -y install podman
>>설치 완료 후, 따로 systemd 설정 할 필요가 없습니다.

2)	사용법 확인
>$ podman run –help

3)	컨테이너 생성
>$ podman run -ti -d --name cont1 httpd
>$ podman run -ti -d --name cont2 httpd
>$ podman run -ti -d --name cont3 httpd
>$ podman run -ti -d --name cont4 httpd

4)	컨테이너 구동 확인
>$ podman ps -a
CONTAINER ID  IMAGE                           COMMAND           CREATED       STATUS                   PORTS  NAMES
54ae076dafdf  docker.io/library/httpd:latest  httpd-foreground  24 hours ago  Exited (0) 24 hours ago         cont4
144f2ef716e4  docker.io/library/httpd:latest  httpd-foreground  24 hours ago  Exited (0) 24 hours ago         cont3
484d65626cd8  docker.io/library/httpd:latest  httpd-foreground  24 hours ago  Exited (0) 24 hours ago         cont2
d3cc517fe534  docker.io/library/httpd:latest  httpd-foreground  24 hours ago  Exited (0) 24 hours ago         cont1

5)	컨테이너 중지, 시작
>중지 : $ podman stop cont1
>시작 : $ podman start cont1

6)	컨테이너 이미지 확인
>$ podman images
7)	컨테이너 삭제
>$ podman rm cont4
------------------------------------------------------------------------------
Centos 8을 이용하여 리눅스 최초 설치 시 기본 설치인 AMP 설치 실습을 해보았습니다.
입사 후 첫 실습으로 했던 기억을 떠올려 실습을 진행하였고, LAMP 설치는 무리없이 진행하였습니다.
pod같은 경우, 개념이 조금 생소하여 이론과 실 사용의 사례들을 공부하도록 하겠습니다.
