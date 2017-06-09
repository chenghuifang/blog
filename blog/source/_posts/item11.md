---
title: 咱们是怎么跨域的？ ---代理
tags: [跨域]
---

#### 什么是代理服务器  
代理服务器，客户机在发送请求时，不会直接发送给目的主机，而是先发送给代理服务器，代理服务接受客户机请求之后，再向主机发出，并接收目的主机返回的数据，存放在代理服务器的硬盘中，再发送给客户机。 
#### 为什么要使用代理服务器 
1）提高访问速度 
由于目标主机返回的数据会存放在代理服务器的硬盘中，因此下一次客户再访问相同的站点数据时，会直接从代理服务器的硬盘中读取，起到了缓存的作用，尤其对于热门站点能明显提高请求速度。 
2）防火墙作用 
由于所有的客户机请求都必须通过代理服务器访问远程站点，因此可在代理服务器上设限，过滤某些不安全信息。 
3）通过代理服务器访问不能访问的目标站点

那什么是正向代理呢，什么是反向代理呢？
#### 正向代理
正向代理 是一个位于客户端和原始服务器(origin server)之间的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并指定目标(原始服务器)，然后代理向原始服务器转交请求并将获得的内容返回给客户端。客户端必须要进行一些特别的设置才能使用正向代理。
#### 反向代理
反向代理正好相反，对于客户端而言它就像是原始服务器，并且客户端不需要进行任何特别的设置。客户端向反向代理的命名空间(name-space)中的内容发送普通请求，接着反向代理将判断向何处(原始服务器)转交请求，并将获得的内容返回给客户端，就像这些内容原本就是它自己的一样。
#### 正向代理和反向代理
简单的区别方法：正向代理就是我们在浏览器可以设置的代理服务器，主动权在浏览者手里。比如我们有时候要查阅一些资料，被国内墙掉了，这时候我可以在国外的服务器上搭建一个nginx正向代理服务器，然后我们就可以通过浏览器设置代理服务器，来翻墙了。反向代理，是浏览者不知情的，服务器端自己假设的。

现在许多大型web网站都用到反向代理。除了可以防止外网对内网服务器的恶性攻击、缓存以减少服务器的压力和访问安全控制之外，还可以进行负载均衡，将用户请求分配给多个服务器。 
Nginx作为近年来较火的反向代理服务器，安装在目的主机端，主要用于转发客户机请求，后台有多个http服务器提供服务，nginx的功能就是把请求转发给后面的服务器，决定哪台目标主机来处理当前请求。
咱们使用的是nginx反向代理
#### nginx反向代理服务器的配置：
```
    server {
        listen       8888;
        server_name  192.168.5.173;
        client_max_body_size    100m;
         
        location / {
            proxy_pass  http://192.168.5.173:8080;
            proxy_set_header    X-Real-IP   $remote_addr;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for; 
        }
        location /ga/ {
            proxy_pass http://192.168.25.11:3000;
            proxy_set_header    X-Real-IP   $remote_addr;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for; 
        }
        location /auth {
            proxy_pass http://192.168.25.11:3000;
            proxy_set_header    X-Real-IP   $remote_addr;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for; 
        }
        location /file {
            proxy_pass http://192.168.25.11:3000;
            proxy_set_header    X-Real-IP   $remote_addr;
            proxy_set_header    Host    $host;
            proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for; 
        }
    }
```
#### 我对正向代理不够了解，就搜了一下（nginx正向代理配置）
```
server{  
        resolver 8.8.8.8;  
        resolver_timeout 30s;   
        listen 82;  
        location / {  
                proxy_pass http://$http_host$request_uri;  
                proxy_set_header Host $http_host;  
                proxy_buffers 256 4k;  
                proxy_max_temp_file_size 0;  
                proxy_connect_timeout 30;  
                proxy_cache_valid 200 302 10m;  
                proxy_cache_valid 301 1h;  
                proxy_cache_valid any 1m;  
        }  
}
```
1、不能有hostname。 
2、必须有resolver, 即dns，即上面的8.8.8.8，超时时间（30秒）可选。 
3、配置正向代理参数，均是由 Nginx 变量组成。
```
proxy_pass $scheme://$host$request_uri;    
proxy_set_header Host $http_host; 
```
4、配置缓存大小，关闭磁盘缓存读写减少I/O，以及代理连接超时时间。  
```
proxy_buffers 256 4k;    
proxy_max_temp_file_size 0;    
proxy_connect_timeout 30;    
```
5、配置代理服务器 Http 状态缓存时间。
```  
proxy_cache_valid 200 302 10m;    
proxy_cache_valid 301 1h;    
proxy_cache_valid any 1m;   
```
配置好后，重启nginx，以浏览器为例，要使用这个代理服务器，则只需将浏览器代理设置为http://+服务器ip地址+:+82（82是刚刚设置的端口号）即可使用了。

