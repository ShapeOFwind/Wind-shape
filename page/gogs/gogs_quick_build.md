# Gogs安装配置(快速搭建版)


[gogs官网](https://gogs.io/)

[oschina gogs介绍](http://www.oschina.net/p/gogs/)

#### 一句话描述：
>一款极易搭建的自助 Git 服务。

###### 环境
> centos7：golang+mysqldb+git

### 安装配置环境
```
yum install mysql-community-server  go  git  -y

配置防火墙 selinux
```

### 安装配置数据库
>这个mysql不允许简单的密码，所以第三条语句我未执行，后面安装时候直接用root作为数据库的用户。gogs推荐使用InnoDB引擎。创建库时候选择utf8. 
```
systemctl start mysqld ;systemctl enable mysqld
//开启数据库服务

cat /var/log/mysqld.log | grep password
//获得mysql root密码

mysql_secure_installation
//初始化数据库 使用上一步获得密码

mysqld -u root -p
//登录mysql

SET GLOBAL storage_engine = ‘InnoDB‘;
CREATE DATABASE gogs CHARACTER SET utf8 COLLATE utf8_bin;
GRANT ALL PRIVILEGES ON gogs.* TO ‘root’@‘localhostIDENTIFIED BY ‘itadmin’;
FLUSH PRIVILEGES;
QUIT；
//SQL语句
```
### 安装配置gogs
```
wget https://dl.gogs.io/0.11.4/linux_amd64.tar.gz
//下载软件包

tar  -zxf  linux_amd64.tar.gz;   mv gogs    /gogs
//解压

useradd git
chown -R  git:git   /gogs
mkdir /gogs-repositories
chown  -R  git:git   /gogs-repositories
//添加git用户 

su git
/gogs/gogs web &
//启动gogs

```

> 最下方配置选项建议点一点做详细配置，如果添加内置SSH避开系统上的22端口，管理员账号不允许admin  避开吧


![image](/img/gogs/001.png)

![image](/img/gogs/002.png)

###### 至此安装结束



[gogs下载地址](https://dl.gogs.io/0.11.4/)

[gogs配置文件手册](https://gogs.io/docs/advanced/configuration_cheat_sheet)

[gogs文档手册](https://gogs.io/docs/)