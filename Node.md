# Node.js

--------------------------------------------------------------------------------

## 安装

推荐用版本管理工具 [nvm](https://github.com/creationix/nvm) 来管理 Node.js

```bash
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
$ source ~/.bashrc
```

之后用 nvm 安装并管理 Node.js

```bash
$ nvm install <version>
$ npm i -g yarn
$ node -v
$ npm -v
```

## 配置

### 查看 registry 地址

```bash
$ npm config list
```

### 配置淘宝源

```bash
# 1 直接修改
$ npm config set registry https://registry.npm.taobao.org
$ yarn config set registry https://registry.npm.taobao.org

# 2 通过编辑配置文件
$ vi ~/.npmrc

# 添加或者修改 registry 地址
registry=https://registry.npm.taobao.org/
```
