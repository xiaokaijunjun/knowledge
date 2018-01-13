#源码安装nginx

###环境：Centos7.4

1.到nginx官网下载最新稳定包1.12.2到桌面<br/>
2.rz命令把下载的nginx压缩包上传到centos的usr/local目录

![](https://i.imgur.com/DJhPwot.png)
3.安装依赖包<br/>
yum -y install gcc-c++ zlib pcre-devel openssl<br/>
说明：<br/>
gcc-c++：编译依赖gcc环境<br/>
zlib：gzip模块需要<br/>
pcre：rewrite重写模块<br/>
openssl：ssl功能需要<br/>
4.解压缩包<br/>
(1)ls查看上传的文件
![](https://i.imgur.com/yCWWFIj.png)
(2)解压<br/>
tar -zxvf nginx-1.12.2.tar.gz<br/>
选项：<br/>
z	&nbsp;&nbsp;针对tar.gz格式的包进行打包或解压<br/>
x	&nbsp;&nbsp;解压<br/>
v   &nbsp;&nbsp;显示详细信息<br/>
f	&nbsp;&nbsp;文件<br/>
![](https://i.imgur.com/eZshwyp.png)<br/>
5.源码安装三部曲-使用configure配置<br/>
(1)进入解压好的nginx文件夹
![](https://i.imgur.com/GjojxoO.png)<br/>
(2)开始配置<br/>
./configure
编译的时候可以自定义一些功能，以下供参考：<br/>
--prefix  &nbsp;&nbsp;&nbsp;&nbsp;指定编译完成后的路径<br/>
--user=www    &nbsp;&nbsp;&nbsp;&nbsp;添加服务的用户www(需存在)<br/>
--group=www   &nbsp;&nbsp;&nbsp;&nbsp;添加服务的用户组www(需存在)<br/>
--with-http_ssl_module  &nbsp;&nbsp;&nbsp;&nbsp;加载ssl模块<br/>
--with-pcre  &nbsp;&nbsp;&nbsp;&nbsp;使用pcre<br/>
6.源码安装三部曲-使用make编译<br/>
make -j 4	代表4个进程同时编译，加快编译速度，看你cpu有几个核心<br/>
7.源码安装三部曲-使用make install安装<br/>
make install<br/>
8.启动nginx<br/>
启动命令：/usr/local/nginx/sbin/nginx<br/>
浏览器输入主机ip查看是否成功<br/>
![](https://i.imgur.com/vsf5hMl.png)<br/>
查看进程：<br/>
![](https://i.imgur.com/eehrfk1.png)<br/>
添加开启启动：编辑vim /etc/rc.local，把启动命令加入即可<br/>
![](https://i.imgur.com/FzkECUj.png)<br/>
关闭命令：/usr/local/nginx/sbin/nginx -s stop<br/>
重启命令：/usr/local/nginx/sbin/nginx -s reload<br/>