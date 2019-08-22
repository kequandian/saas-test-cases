## etcd使用
### 说明
* etcd单实例部署在虚拟机（192.168.3.28）
* etcd版本v3.3.13
* etcd对外开放端口：2379

### etcd-client getway使用（[查看swagger](http://192.168.3.28:8088/swagger-ui.html#/etcd-endpoint)）
```
# post
request:
  http://192.168.3.28:8088/api/etcd
requestBody:
  {"key":"/name","value":"hello"}
response:
  {
    "code": 200,
    "data": {
        "createRevision": "0",
        "key": "",
        "lease": "0",
        "modRevision": "0",
        "value": "",
        "version": "0"
    },
    "message": "Success"
}

# get
request:
  http://192.168.3.28:8088/api/etcd?key=/name
response:
  {
    "code": 200,
    "data": {
        "createRevision": "127",
        "key": "/name",
        "lease": "0",
        "modRevision": "127",
        "value": "hello",
        "version": "1"
    },
    "message": "Success"
}
```

### etcd-client使用 
**添加依赖**
```
<dependency>
    <groupId>com.jfeat</groupId>
    <artifactId>etcd-client</artifactId>
    <version>1.0.0</version>
</dependency>
```

在application.yml添加配置
```
etcd:
  etcdEndpoints: http://192.168.3.28:2379   // etcd端口，多个用“,”隔开
  serviceName: cr-sys                        // 服务名称
  serviceEndpoint: http://127.0.0.1:8081     // 服务地址
  provideService: false                      // 是否对外提供服务
  subscribeServices: uaas                    // 订阅服务，多个用“,”隔开
```
*说明：etcd-client不支持服务多实例模式，如有运行异常，留意配置文件及日志信息*
