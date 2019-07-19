## etcd使用
### 说明
* etcd单实例部署在虚拟机（192.168.2.122）
* etcd版本v3.3.13
* etcd对外开放端口：2379

### etcd getway使用
```
# put
curl -L http://192.168.2.122:2379/v3beta/kv/put -X POST -d '{"key": "name", "value": "lili"}'
{"header":{"cluster_id":"14841639068965178418","member_id":"10276657743932975437","revision":"11","raft_term":"10"}}

# get
curl -L http://192.168.2.122:2379/v3beta/kv/range -X POST -d '{"key": "name"}'
# {"header":{"cluster_id":"14841639068965178418","member_id":"10276657743932975437","revision":"11","raft_term":"10"},"kvs":[{"key":"name","create_revision":"10","mod_revision":"10","version":"1","value":"lili"}],"count":"1"}
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
  etcdEndpoints: http://192.168.2.122:2379   // etcd端口，多个用“,”隔开
  serviceName: cr-sys                        // 服务名称
  serviceEndpoint: http://127.0.0.1:8081     // 服务地址
  provideService: false                      // 是否对外提供服务
  subscribeServices: uaas                    // 订阅服务，多个用“,”隔开
```
*说明：etcd-client不支持服务多实例模式，如有运行异常，留意配置文件及日志信息*
