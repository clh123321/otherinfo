### 1，网上查找的方法
```
C:\Users\zouqj>e:
E:\>cd E:\Redis-x64-3.2.100
E:\Redis-x64-3.2.100>redis-server --service-install redis.windows.conf --loglevel verbose --service-name redis --port 6379
```

### 2,指定端口
```
cd d:xxx/xxx
cd
redis-server --service-install redis.windows-service.conf --service-name Redis6381 --port 6381
```
### 3,集群
redis-trib.rb create --replicas 1 127.0.0.1:6379 127.0.0.1:6300 127.0.0.1:6301 127.0.0.1:6302 127.0.0.1:6303 127.0.0.1:6304