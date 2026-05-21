# mysql-study
用于上传mysql的学习记录
下载官网mysqlyum安装包
最小化安装的centos7系统怎么和本地物理机传输文件
在xshell 工具使用lrzsz  rz上传，sz下载
yum install -y mysqlyum安装包
vim /etc/yum.repos.d/mysql-community-repo
选择安装版本
yum makecache  刷新缓存
yum install -y mysql-community*
systemctl start mysqld启动服务
grep password /var/log/mysqld.log查看临时密码

2026-5-21
给mysql改密码时的报错
unable to change password; error: 'Your password does not satisfy the current policy requirements'
先登录mysql  mysql -u root -p

--1改密码：
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Root_1234';

删除安全组件
UNINSTALL COMPONENT 'file://component_validate_password';
改为想要的简单密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Root_1234';

源码安装mysql 
1.先安装ftp  yum install -y vsftpd
2/创建主目录
3/下载yum仓库的包
4/仅下载不安装  --downloadonly
5/找到下载好的mysql安装包
find /var/cache/yum/x86_64/7/ -iname "*.rpm" -exec cp -rf {} /var/ftp/mysql57 \
6/创建依赖关系
	cd /var/ftp/mysql57
	yum provides createrepo
	yum install -y createrepo
	createrepo /var/ftp/mysql57/
7/FTP启动

客户机端操作
1/自建yum仓库  vim /etc/yum.repos.d/mysql57.repo
[mysql57]
name=leileiftp
baseurl=ftp://服务器ip/mysql57
gpgcheck=0
enabled=1
2/安装  yum makecache  刷下缓存
yum install -y mysql-community-server

MySQL的使用
建库 create database 数据库名；
建表 create tabale 表名 (列名  类型 ，列名 类型)；
增 insert into 表名 values (1)；
删
改
查 select * from 表名；