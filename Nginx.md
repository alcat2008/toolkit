# Nginx

--------------------------------------------------------------------------------

## 安装

```shell
brew install nginx
```

## 启动

```shell
sudo nginx #打开
sudo nginx -s reload|reopen|stop|quit  #重新加载配置|重启|停止|退出
sudo nginx -t   #测试配置是否有语法错误
```

## 测试

```shell
http://localhost:8080
```

## 配置

```shell
/usr/local/etc/nginx/nginx.conf
```

### SPA 路由

现在 Web 项目基本上都是单页面应用（SPA），其路由是内部控制，需要在 nginx 做特殊配置支持。

```shell
location / {
  index  index.html index.htm;
  try_files $uri $uri/ /index.html;
}
```

### gzip

默认情况下，nginx 的 gzip 压缩是关闭的。

```shell
## Compression
gzip                on;
gzip_min_length     1024;
gzip_buffers        4 8k;
gzip_comp_level     3;
gzip_http_version   1.0;
gzip_disable        "msie6";
gzip_types          text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript image/x-icon image/jpeg image/bmp image/png image/gif;
gzip_vary           on;
```

具体说明：

- gzip_min_length

  最小压缩的页面，如果页面过于小，可能会越压越大，这里规定大于1K的页面才启用压缩。

- gzip_buffers

  设置系统获取几个单位的缓存用于存储gzip的压缩结果数据流。

- gzip_comp_level

  压缩级别，1压缩比最小处理速度最快，9压缩比最大但处理最慢，同时也最消耗CPU，一般设置为3就可以了。

- gzip_types

  什么类型的页面或文档启用压缩。

###  强制使用 https (http 跳转到 https)

将所有的 http 请求通过 rewrite 重写到 https

```shell
server {
    listen       80;
    server_name  <域名>;

    rewrite ^(.*)$    https://$host$1    permanent;
}
```

### 使用 proxy_pass 反向代理时，cookie 丢失的问题

1. 如果只是host、端口转换，则cookie不会丢失。例如：

```shell
location /project {
  proxy_pass   http://127.0.0.1:8080/project;
}  
```

通过浏览器访问http://127.0.0.1/project时，浏览器的cookie内有jsessionid。再次访问时，浏览器会发送当前的cookie。

2. 如果路径也变化了，则需要设置cookie的路径转换，nginx.conf的配置如下
    location /proxy_path {
        proxy_pass   http://127.0.0.1:8080/project;
    }

通过浏览器访问http://127.0.0.1/proxy_path时，浏览器的cookie内没有jsessionid。再次访问时，后台当然无法获取到cookie了。
详细看了文档：http://nginx.org/en/docs/http/ngx_http_proxy_module.html?&_ga=1.161910972.1696054694.1422417685#proxy_cookie_path

加上路径转换：`proxy_cookie_path  /project /proxy_path`;

则可以将project的cookie输出到proxy_path上。正确的配置是：

```shell
location /proxy_path {
  proxy_pass   http://127.0.0.1:8080/project;
  proxy_cookie_path  /project /proxy_path;
}
```
