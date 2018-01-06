# 搭建shadowsocks

###环境：Centos7.4 
自己动手搭建shadowsocks翻墙服务
---
已有国外vps

安装shadowsocks：
pip install shadowsocks

编辑配置文件：vim /etc/shadowsocks.json<br/>
{ <br/>
"server":"my_server_ip", 		#vps ip地址  
"server_port":8388,<br/>
 "local_address":"127.0.0.1", <br/>
"local_port":1080, <br/>
"password":"mypassword", <br/>
"timeout":300, <br/>
"method":"aes-256-cfb", <br/>
"fast_open": false<br/>
}

多用户配置：<br/>
{ 
"server": "0.0.0.0", <br/>
"port_password": <br/>
{ "8381": "foobar1",<br/>
  "8382": "foobar2", <br/>
"8383": "foobar3", <br/>
"8384": "foobar4" <br/>
}, <br/>
"timeout": 300, <br/>
"method": "aes-256-cfb" }<br/>

防火墙开放8388 80端口:<br/>
firewall-cmd --zone=public --add-port=80/tcp --permanent<br/>
firewall-cmd --zone=public --add-port=8382/tcp --permanent<br/>
重启防火墙:<br/>
systemctl restart firewalld.service

后台运行命令：<br/>
ssserver -c /etc/shadowsocks.json -d start <br/>
停止服务：<br/>
ssserver -c /etc/shadowsocks.json -d stop

开机启动
在/etc/rc.local中加入
sudo ssserver -c /etc/shadowsocks.json -d start

window 使用shandowsocks<br/>
![](https://i.imgur.com/QkG54b8.png)