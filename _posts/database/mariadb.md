mariadb 설치 및 제거

https://www.buyprotheme.com/uninstall-mysql-from-ubuntu-and-install-mariadb/


root 비밀번호 설정

https://websiteforstudents.com/reset-mariadb-root-password-ubuntu-17-04-17-10/



```bash
sudo netstat -antp | grep mysql
```

mysql의 연결 정보를 확인할 수 있다.
이때 IP가 127.0.0.1:3306으로 되어있으면 로컬호스트에서만 접속이 가능하다. 다른 IP에서도 접속이 가능하려면 다음과 같이 변경해야 한다.



```bash
sudo vi /etc/mysql/my.cnf
```

bind-address 를 0.0.0.0으로 바꾸고 mysql을 다시 실행

```bash
sudo service mysql restart
```



