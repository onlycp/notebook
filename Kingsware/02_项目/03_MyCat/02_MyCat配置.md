

1. 创建原型库用户

```mysql
# 登录MySql
mysql -u root -p
# 创建mycat用户
create user 'mycat'@'%' IDENTIFIED BY 'MyCat.123456';
GRANT XA_RECOVER_ADMIN ON *.* TO 'root'@'%';
GRANT ALL PRIVILEGES ON *.* TO 'mycat'@'%';
# 刷新权限
flush privileges;
```

2. 配置`datasources/prototypeDs.datasource.json`

```json
{
	"dbType":"mysql",
	"idleTimeout":60000,
	"initSqls":[],
	"initSqlsGetConnection":true,
	"instanceType":"READ_WRITE",
	"maxCon":1000,
	"maxConnectTimeout":30000,
	"maxRetryCount":5,
	"minCon":1,
	"name":"prototypeDs",
	"password":"MyCat.123456",
	"type":"JDBC",
	"url":"jdbc:mysql://10.11.2.95:3306/mysql?useUnicode=true&serverTimezone=Asia/Shanghai&characterEncoding=UTF-8",
	"user":"mycat",
	"weight":0
}

```

3. 配置MyCat访问用户`users/root.user.json`

```json
{
	"dialect":"mysql",
	"ip":null,
	"password":"123456",
	"transactionType":"proxy",
	"username":"root"
}
```



