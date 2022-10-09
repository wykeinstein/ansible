# 说明
使用该role，可以根据传入的数据渲染出nginx的基于ip地址的虚拟主机配置文件，一个服务一个nginx的配置文件
* role解析的数据结构模板如下：
```
---
project_name: project_test
test_services:
  test_service:
    group: test1
    port: 8080
    conf_path: /root/test_conf
    nginx:                          
      upstream: testupstream        
      mode:                         
      location_path: "/test/"       
      proxy_path: "/test/"          
      location_reg: "^~"            
      proxy_set_header:             
        - "Host $http_host"
        - "X-Real-IP $remote_addr"
        - "X-Forwarded-For $proxy_add_x_forwarded_for" 
```
* template模板中的变量和nginx这个数据结构的对应关系如下：
```
nginx:                          --> nginx
  upstream: testupstream        --> nginx.upstream
  mode:                         --> nginx.mode
  location_path: "/test/"       --> nginx.location_path
  proxy_path: "/test/"          --> nginx.proxy_path
  location_reg: "^~"            --> nginx.location.reg
  proxy_set_header:             --> nginx.proxy_set_header
    - "Host $http_host"
    - "X-Real-IP $remote_addr"
    - "X-Forwarded-For $proxy_add_x_forwarded_for" 
```
