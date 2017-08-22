# Mongodb

--------------------------------------------------------------------------------


## 安装

参考 [官网说明](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

## 运行

后台

```
# mongod
```

## 配置

```
# mongo

> use admin
> db.createUser({ user: 'xxx', pwd: 'xxx', roles: [{ role: 'root', db: 'admin' }] })
> db.auth('xxx', 'xxx')

# mongo -u xxx -p xxx admin
```
