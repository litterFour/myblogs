##### storeage

![logo](./images/storage.jpg ':size=WIDTHxHEIGHT')

刷新浏览器，sessionStorage是否清空

https://blog.csdn.net/gulang03/article/details/88210979

浏览器刷新的三种方式 刷新了什么 （storage）

 
    200 form memory cache:  不访问服务器，资源缓存在内存中。浏览器关闭后 资源被释放
    200 from disk cache:   不访问服务器，资源缓存在硬盘，浏览器关闭  资源依然存在
    304 Not Modified: 访问服务器，发现数据没有更新，服务器返回此状态码。然后从缓存中读取数据。
    三级缓存原理：
    1. 先去内存看，如果有，直接加载
    2. 如果内存没有，择取硬盘获取，如果有直接加载
    3. 如果硬盘也没有，那么就进行网络请求
    4. 加载到的资源缓存到硬盘和内存
    比如：访问图片-> 200 -> 退出浏览器
    再进来-> 200(from disk cache) -> 刷新 -> 200(from memory cache)
    CND 缓存
    http://kms.sf-express.com/KMS/learning/viewCourses_init.action?isManager=&coursesVo.id=246858&learnTaskId=
    强缓存：不向服务器发请求。expires/http 1.0   cache-control/http 1.1
    协商缓存(304 not Modified)：向服务器发请求：[last-Modified，If-Modified-since] [ETag,If-None-Match]
    分布式系统里多台机器间的文件Last-Modified必须保持一致，以免负载均衡到不同机器导致比对失败；
    分布式系统尽量关掉Etag（每台机器生成的Etag都会不一样）
    浏览器在第一次访问页面时向服务器请求资源，并缓存起来，下次再访问时会判断在缓存中是否已有该资源且有没有更新过，如果已有该资源且未更新过，则直接从浏览器缓存中读取。原理：通过HTTP 请求头中的 If-Modified-Since（If-No-Match） 和响应头中的Last-Modified（ETag）来实现，HTTP请求把 If-Modified-Since（If-No-Match）传给服务器，服务器将其与Last-Modified（ETag）对比，若相同，则文件没有被改动过，则返回304，直接浏览器缓存中读取资源即可。虽然该方法减少了已缓存资源的下载时间，但仍然发起了一次http请求。
    解决：已缓存资源不再发起http请求，即HTTP的Expires和Cache-Control。对一个网站而言，CSS、JavaScript、图片等静态资源更新的频率都比较低，而这些文件又几乎是每次HTTP请求都需要的，如果将这些文件缓存在浏览器中，可以极好的改善性能。通过设置http头中的cache-control和expires的属性，可设定浏览器缓存，将静态内容设为永不过期，或者很长时间后才过期。

 
 
