# Nginx 负载均衡 load balance

## 实际例子

后端服务器扩容，利用 nginx 作为负载均衡


文件 hellotest.xxxxx.net.conf

```shell
upstream ocr-lb {
    server 172.xx.xx.xx1:5046;
    server 172.xx.xx.xx2:5046;
}

server {
        listen 443 ssl;
        ssl_certificate xxxx_xxxx.net.pem;
        ssl_certificate_key xxxx_xxxx.net.key;
        server_name xxxxtest.xxxx.net;

		location /api/ocr/ {
             proxy_pass http://ocr-lb;
        }
}
```

nginx 默认使用 round-robin 负载均衡算法。
实际使用过程中并非严格 50:50，而是一段时间大量请求落在server1 少部分在server2，另一段时间反过来。

## 配合 docker 使用

```shell
docker cp hellotest.xxxxx.net.conf nginx:/etc/nginx/conf.d/
docker exec nginx nginx -s reload

```


## 额外情况

nginx load balance ， upstream {name} name 里不能包含 下划线 https://bz.apache.org/bugzilla/show_bug.cgi?id=62371#c14 18年由于安全漏洞的分析报告而加上的限制。

