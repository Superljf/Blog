- nginx.exe -s reload
- nginx -s stop       快速关闭Nginx，可能不保存相关信息，并迅速终止web服务。 
  
  - 检查配置文件是否有误 nginx -t
  
  - ```js
    nginx -s reload  # 向主进程发送信号，重新加载配置文件，热重启
    nginx -s reopen     # 重启 Nginx
    nginx -s stop    # 快速关闭
    nginx -s quit    # 等待工作进程处理完成后关闭
    nginx -T         # 查看当前 Nginx 最终的配置
    nginx -t -c <配置路径>    # 检查配置是否有问题，如果已经在配置目录，则不需要-c
    ```
  
    

![image-20200326135150803](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200326135150803.png)

![image-20200326140041414](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200326140041414.png)



![img](https://user-gold-cdn.xitu.io/2020/3/25/17110141b0a9e71f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

![image-20200330143210792](C:\Users\SuperLjf\AppData\Roaming\Typora\typora-user-images\image-20200330143210792.png)

#### nginx支持的负载均衡调度算法方式如下：

- weight  轮询（默认）：接收到的请求按照顺序逐一分配到不同的后端服务器，即使在使用过程中，某一台后端服务器宕机，nginx会自动将该服务器剔除出队列，请求受理情况不会受到任何影响。 这种方式下，可以给不同的后端服务器设置一个权重值（weight），用于调整不同的服务器上请求的分配率；权重数据越大，被分配到请求的几率越大；该权重值，主要是针对实际工作环境中不同的后端服务器硬件配置进行调整的。

- ip_hash：每个请求按照发起客户端的ip的hash结果进行匹配，这样的算法下一个固定ip地址的客户端总会访问到同一个后端服务器，这也在一定程度上解决了集群部署环境下session共享的问题。

- fair：智能调整调度算法，动态的根据后端服务器的请求处理到响应的时间进行均衡分配，响应时间短处理效率高的服务器分配到请求的概率高，响应时间长处理效率低的服务器分配到的请求少；结合了前两者的优点的一种调度算法。但是需要注意的是nginx默认不支持fair算法，如果要使用这种调度算法，请安装upstream_fair模块

- url_hash：按照访问的url的hash结果分配请求，每个请求的url会指向后端固定的某个服务器，可以在nginx作为静态服务器的情况下提高缓存效率。同样要注意nginx默认不支持这种调度算法，要使用的话需要安装nginx的hash软件包
  ————————————————

#### 动静分离配置

![img](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4756ac5f0b9c4f5580df8131691f6f42~tplv-k3u1fbpfcp-zoom-1.image)

https://juejin.im/post/6862180797005332493