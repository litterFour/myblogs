#### docker

docker只是容器，就好像虚拟机，只是个操作系统环境，给你安装自己的软件和服务。 k8s是个集群，可以和很多负载均衡产品（云产品）一起集成。 k8s的ingress控制器可以支持一些开源的负载均衡器，除了nginx，还有Haproxy等。 nginx具有反向代理功能，可以很容易实现反向代理的负载均衡，而且也比较流行，轻便，所以集群里用的也比较多。但是不是说非要用nginx才能实现负载均衡。

https://blog.csdn.net/qq_33774822/article/details/84260800

https://blog.csdn.net/yanyf2016/article/details/102593133
