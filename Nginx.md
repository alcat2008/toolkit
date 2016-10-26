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
