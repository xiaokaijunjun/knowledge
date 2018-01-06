# 搭建shadowsocks #

###环境：Centos7.4 
自己动手搭建shadowcosks翻墙服务
---
已有国外vps

安装shadowsocks：
pip install shadowsocks

编辑配置文件：vim /etc/shadowsocks.json

{ 
"server":"my_server_ip", 		#vps ip地址
"server_port":8388,
 "local_address":"127.0.0.1", 
"local_port":1080, 
"password":"mypassword", 
"timeout":300, 
"method":"aes-256-cfb", 
"fast_open": false
}

多用户配置
{ 
"server": "0.0.0.0", 
"port_password": 
{ "8381": "foobar1",
  "8382": "foobar2", 
"8383": "foobar3", 
"8384": "foobar4" 
}, 
"timeout": 300, 
"method": "aes-256-cfb" }

防火墙开放8388 80端口
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=8382/tcp --permanent
重启防火墙
systemctl restart firewalld.service

后台运行命令：
ssserver -c /etc/shadowsocks.json -d start ssserver -c /etc/shadowsocks.json -d stop

开机启动
在/etc/rc.local中加入
sudo ssserver -c /etc/shadowsocks.json -d start

window 使用shandowsocks
![](https://i.imgur.com/QkG54b8.png)