惨痛教训-数据库被删掉



查看日志

/var/log/secure

发现了很多 登录请求。估计是被撞库攻击。

做以下防范:

1.更改ssh端口

2.更改mysql端口

3.打开mysql 操作日志

更改ssh端口:

vim /etc/ssh/sshd\_config  

打开Port 2323

重启服务:

/bin/systemctl restart  sshd.service  



打开防火墙端口:

firewall-cmd --permanent --add-port=2323/tcp

 重载服务器

firewall-cmd --reload



