!> 10-29
    

`F5`: https://www.sohu.com/a/300651868_671058

`tunnel`: 

`gitlab cli`、

* cookie【存在客户端】【域名相同】

 

* session【会话】Session是对于服务端来说的，Session是服务器和客户端建立连接时添加的一个客户端连接标志，最终在服务器软件（Apache、Tomcat、JBoss）转化为一个临时的Cookie发送给客户端，当客户端第一次请求服务器时，会检查是否携带了这个Session（临时Cookie），如果没有则会添加Session，如果有就拿出这个Session来做相关操作。每隔session有个唯一的sessionId。

  大部分的Session机制都使用进程中Cookie来保存Session id的，关闭浏览器后这个进程也就自动消失了，进程中的Cookie自然就消失了，那么Session id也跟着消失了，再次连接到服务器时也就无法找到原来的Session了。也有使用硬盘中Cookie，比如说CSDN的“记住我一周”，或者我们的购物车信息可以在切换不同浏览器时依然可用。这就要用到我们上文提到的另一种Cookie了——硬盘中Cookie，这时Session id将长期保存在硬盘上的Cookie中，直到失效为止。

* token:【令牌】

  uid(用户唯一的身份标识)
   time(当前时间的时间戳)
   sign(签名，由token的前几位+盐以哈希算法压缩成一定长的十六进制字符串，可以防止恶意第三方拼接token请求服务器)。
   还可以把不变的参数也放进token，避免多次查库。

  1、用户登录，服务器生成token，服务器保存token，并且返回给客户端

  2、客户端保存token，下次请求 携带token

  3、对比本地和数据库token

---

`cookie：存在客户端,存储容量有限，用户可见\可更改\不安全`

`session：存储在服务端`, sessionId

状态码：

https://www.cnblogs.com/xflonga/p/9368993.html

http://nodejs.cn/api/http.html#responsereq

https://www.runoob.com/http/http-status-codes.html

```
```
路由

svg icon ：

  https://segmentfault.com/a/1190000015367490

  https://www.jianshu.com/p/70f9c9268c83

gitlab  role

login

cookie同源： https://www.sohu.com/a/272360134_465223

https://www.cnblogs.com/liaojie970/p/7606168.html

https://blog.csdn.net/stpeace/article/details/82823686

  浏览器提交的Cookie需要满足以下两点：

```
1.当前域名或者父域名下的Cookie；
2.当前路径或父路径下的Cookie
```

和session

session 分布式  web容器

token（令牌） 请求 

web容器 和 web服务器     浏览器容器



https://www.cnblogs.com/l199616j/p/11195667.html

添加水印   、  国际化



**hash模式和history模式的不同** ：

https://www.cnblogs.com/makai/p/12373268.html

https://www.cnblogs.com/l199616j/category/1388685.html



控制台调试



CDN和负载均衡

https://www.cnblogs.com/l199616j/p/11195667.html


**hash模式和history模式的不同** ：

https://www.cnblogs.com/makai/p/12373268.html

https://www.cnblogs.com/l199616j/category/1388685.html



控制台调试

 