# Linux 环境 curl 命令

参考资料

[阮一峰 curl 初学教程][1]  
[阮一峰 curl 用法指南][2]  

## 初学教程比较简单，  
-v -I/i -o -L -X( GET/ POST/ ...)  -A/-H   
--header --user-agent --referer --cookie (相关-c/-b) --user   

## 用法指南 有些更好的例子。 

POST 请求数据 中包含空格 urlencode。 
```shell
$ curl --data-urlencode 'comment=hello world' https://google.com/login“
```

## 大佬也是翻译

[curl cookbook][3]

[1]: [http://www.ruanyifeng.com/blog/2011/09/curl.html]
[2]: [https://www.ruanyifeng.com/blog/2019/09/curl-reference.html]
[3]: [https://catonmat.net/cookbooks/curl]