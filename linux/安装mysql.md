#安装mysql
###环境Centos7.4

说明：首先CentOS7 已经不支持mysql，因为收费所以内部集成了mariadb,CentOS7的yum源中默认是没有mysql的。为了解决这个问题，我们要先下载mysql的repo源<br/><br/>
1.从mysql官网下载一个centos7的rpm源<br/>
wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
![](https://i.imgur.com/iCUAa9l.png)
2.安装rpm包，生成mysql的yum源<br/>
rpm -ivh mysql57-community-release-el7-11.noarch.rpm<br/>
![](https://i.imgur.com/Nsz4ij1.png)
3.查看生成mysql的yum源<br/>
![](https://i.imgur.com/6KOGQOl.png)
4.安装mysql
yum -y install mysql-server
![](https://i.imgur.com/PNEpIbp.png)
5.启动mysql服务，systemctl start mysqld.service,发现报错如图
![](https://i.imgur.com/0pK4p8O.png)
解决办法：
(1)查看错误日志 less /var/log/mysql.log
![](https://i.imgur.com/Zgrx7rg.png)
找到问题所在，提示ibdata1这个文件没有写入权限，该文件位于/var/lib/mysql
![](https://i.imgur.com/5vqD7Kf.png)
(2)给mysql文件夹授权<br/>
chmod 777 -R /var/lib/mysql
6.再次启动mysql服务，服务已经起来
![](https://i.imgur.com/az7MOqd.png)
7.运行mysql_secure_installation设置密码或者查看/var/log/mysqld.log会生成一个临时密码<br/>
8.mysql -u root -p 登录mysql
