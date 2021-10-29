#### git代理服务器

!> 443错误码 ---> 解决方案： 检查代理

* 设置http、https代理
```
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'
```
* 查看http、https代理
```
git config --global --get http.proxy
git config --global --get https.proxy
```
* 取消http、https代理
```
git config --global --unset http.proxy
git config --global --unset https.proxy
```
