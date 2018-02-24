# mysql远程连接

## 简介

需要在服务器上开启mysql服务。并且允许远程连接。

* 登陆mysql
* ```
  mysql -uroot -p
  ```
* 添加远程用户
* ```
  grant all on *.* to root@'%' identified by '123456' with grant option;
  flush privileges;


  允许任何ip地址(%表示允许任何ip地址)的电脑用root帐户和密码(123456)来访问这个mysql server。
  ```
* 开放防火墙端口\(这里使用firwall作为防火墙，也有iptables的方式\)
* ```
  firewall-cmd --zone=public --add-port=3306/tcp --permanent
  firewall-cmd --reload
  ```



