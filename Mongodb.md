# Mongodb

--------------------------------------------------------------------------------

## 安装

参考官网 [install-mongodb-on-red-hat](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/)

### Linux

```bash
# 配置 Repo
$ vi /etc/yum.repos.d/mongodb-org-3.6.repo

# repo 内容 -- Start
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
# repo 内容 -- End

# 安装
$ yum install -y mongodb-org

# 启动|关闭|重启
$ service mongod start|stop|restart

# 开机启动
$ chkconfig mongod on

# 连接
$ mongo --host <host>:27017 -u <user> -p <password> <dbname>
```

### Mac

```bash
# 安装
$ brew update
$ brew install mongodb

# 启动
$ mongod

# 连接
$ mongo --host <host>:27017 -u <user> -p <password> <dbname>
```

## 常用命令

命令行下可以使用 `TAB` 键查看联想

```bash
> use <dbname>
> show users                      # 显示当前所有用户
> db.createUser({ user: '<username>', pwd: '<password>', roles: [{ role: 'readWrite', db: '<dbname>' }] })
> db.auth('<username>', '<password>')


> help
> db.help()                       # db详细帮助
> db or db.getName()              # 获取当前使用的数据库名称
> db.serverStatus()               # 服务器的状态
> show dbs                        # 数据库列表
> show collections                # 当前数据库下的所有集合
> db.<collectionname>.help()      # 集合详细帮助
> db.<collectionname>.find()      # 集合里的数据
> db.<collectionname>.count()
> db.<collectionname>.remove({})
> db.dropDatabase()                # 删除当前使用的数据库
> db.stats()                       # 当前db状态
> db.getMongo()                    # 当前db的链接地址
```

## 备份与恢复

```bash
# 备份
$ mongodump -h <host> -d <dbname> -o <dbdirectory>

# 恢复
$ mongorestore -h <host> -d <dbname> --dir <dbdirectory>
```

## 重置密码

```bash
$ vi /etc/mongodb.conf          # 修改 mongodb 配置，将 auth = true 注释掉，或者改成 false
$ service mongodb restart       # 重启 mongodb 服务
 
$ mongo                          # 运行客户端（也可以去mongodb安装目录下运行这个）
> use admin                      # 切换到系统帐户表
> db.system.users.find()         # 查看当前帐户（密码有加密过）
> db.system.users.remove({})     # 删除所有帐户
> db.addUser('admin','password') # 添加新帐户
 
$ vi /etc/mongodb.conf           # 恢复 auth = true
$ service mongodb restart        # 重启 mongodb 服务
```
