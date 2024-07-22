### 一、 安装yum源

1.  下载rpm的repo源

```sh
wget https://repo.mysql.com//mysql80-community-release-el7-11.noarch.rpm
```

2.  安装repo源

```sh
rpm -ivh mysql80-community-release-el7-11.noarch.rpm
```

3.  刷新yum cache

```
yum clean all
yum makecache
```

###  二、 安装MySql

1. 安装Server

```sh
yum install -y mysql-community-server
```

2.  启动服务

```
# 启动
systemctl start mysqld.service
```

3.  找到初始密码

```sh
# 找到初始密码
cat /var/log/mysqld.log | grep password
```

4. 修改密码

```
# 进入MySql
mysql -u root -p
# 修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Abc.1234';
```

5. 调整访问权限

```
# 调整为所有机器可以访问
update user set host='%' where user='root';
# 刷新权限
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```



