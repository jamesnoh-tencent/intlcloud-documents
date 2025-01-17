标准版包括用户自建的单机、主从模式以及腾讯云数据库 Redis 内存版（标准架构），本文为您介绍标准版 Redis 迁移至腾讯云数据库Redis 内存版（集群架构）的兼容性相关内容。

## [兼容性说明](id:jrxsm)
腾讯云数据库 Redis 内存版（集群架构）采用自研 Proxy 加社区集群版的架构，100%兼容社区 Redis Cluster 的命令。
![](https://main.qcloudimg.com/raw/6149cc0a09ba53ab367f5956c8a783b8.jpg)

标准版迁移至内存版（集群架构）面临的最大问题为命令是否兼容内存版（集群架构）的使用规范，内存版（集群架构）使用规范主要注意事项如下：

### 多 KEY 操作
Redis 内存版（集群架构）通过 HASH 算法将 Key 分布至16000个 SLOT，原理可参考 [Redis Cluster 文档](https://redis.io/topics/cluster-spec)。
- 社区 Redis Cluster：不支持任何跨 SLOT 的多 Key 访问命令。
- 腾讯云数据库 Redis 内存版（集群架构）：支持 MGET、MSET、DEL 命令的跨 SLOT 多 Key 访问，主要原理是通过腾讯云自研 Proxy 实现多个节点的命令聚合运算。
- Hash Tag：业务可以通过 Hash Tag 的方式，将需要进行多 Key 运算的 Key 聚合至相同 SLOT，Hash Tag 的使用方式请参考 [Redis Cluster 文档](https://redis.io/topics/cluster-spec)。
- 跨 SLOT 命令列表：

| 命令族         | 命令          | 内存版（集群架构）跨 Slot 支持 |
| -------------- | ------------- | ------------------ |
| keys 族        | del           | ✓                  |
| keys 族        | exists        | ✓                  |
| keys 族        | rename        | x                  |
| keys 族        | renamenx      | x                  |
| keys 族        | unlink        | x                  |
| list 族        | rpoplpush     | x                  |
| list 族        | blpop         | x                  |
| list 族        | brpop         | x                  |
| list 族        | brpoplpush    | x                  |
| sets 族        | sdiff         | x                  |
| sets 族        | sdiffstore    | x                  |
| sets 族        | sinter        | x                  |
| sets 族        | sinterstore   | x                  |
| sets 族        | smove         | x                  |
| sets 族        | sunion        | x                  |
| sets 族        | sunionstore   | x                  |
| sorted sets 族 | zinterstore   | x                  |
| sorted sets 族 | zunionstore   | x                  |
| strings 族     | bitop         | x                  |
| strings 族     | mget          | ✓                  |
| strings 族     | mset          | ✓                  |
| strings 族     | msetnx        | x                  |
| hyperloglog 族 | pfcount       | x                  |
| hyperloglog 族 | pfmerge       | x                  |
| scripting 族   | eval          | x                  |
| scripting 族   | evalsha       | x                  |
| scripting 族   | script exists | x                  |
| Stream 族      | xread         | x                  |
| Stream 族      | xreadgroup    | x                  |

### LUA 支持
- 内存版（集群架构）支持 LUA 命令，但 LUA 脚本中访问的 Key 不能跨 SLOT。
- EVAL、EVALSHA 命令必须要传Key 参数，否则命令将无法执行。
- SCRIPT 的子命令 LOAD、FLUSH、KILL、EXIST 会通过 Proxy 分发至集群中所有的主节点。
```
> eval "return {KEYS[1],KEYS[2],ARGV[1],ARGV[2]}" 2 key1 key2 first second
1) "key1"
2) "key2"
3) "first"
4) "second"
```
>?LUA 使用时必须传参数 key1、key2。

### 事务支持
- 内存版（集群架构）支持事务，但是事务中的命令不能跨 SLOT 访问 Key。
- 当前线上版本需要先执行 watch key 命令，再执行 multi、exec，后续版本会进行优化，免除先执行 watch key 的动作。

### [自定义命令](id:zdyml)
Redis 内存版（集群架构）通过 VIP 封装，在集群模式下提供了标准版的使用体验，对业务的使用带来很大便利，但是对运维不够透明，因此通过自定义命令来弥补这些空缺，支持集群中每个节点的访问，支持方式为在原有命令的参数列表最右边新增一个参数“节点ID”，COMMAND arg1 arg2 ... [节点ID]，节点 ID 可通过 cluster nodes 命令，或者在 [控制台](https://console.cloud.tencent.com/redis) 中获取。
```
10.1.1.1:2000> cluster nodes25b21f1836026bd49c52b2d10e09fbf8c6aa1fdc 10.0.0.15:6379@11896 slave 36034e645951464098f40d339386e9d51a9d7e77 0 1531471918205 1 connectedda6041781b5d7fe21404811d430cdffea2bf84de 10.0.0.15:6379@11170 master - 0 1531471916000 2 connected 10923-1638336034e645951464098f40d339386e9d51a9d7e77 10.0.0.15:6379@11541 myself,master - 0 1531471915000 1 connected 0-546053f552fd8e43112ae68b10dada69d3af77c33649 10.0.0.15:6379@11681 slave da6041781b5d7fe21404811d430cdffea2bf84de 0 1531471917204 3 connected18090a0e57cf359f9f8c8c516aa62a811c0f0f0a 10.0.0.15:6379@11428 slave ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 0 1531471917000 2 connectedef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171 10.0.0.15:6379@11324 master - 0 1531471916204 0 connected 5461-10922

原生命令：info server
自定义命令:
info server ef3cf5e20e1a7cf5f9cc259ed488c82c4aa17171SCAN 
命令示例：
scan 0 238b45926a528c85f40ae89d6779c802eaa394a2
scan 0 match a* 238b45926a528c85f40ae89d6779c802eaa394a2KEYS 
命令示例：
keys a* 238b45926a528c85f40ae89d6779c802eaa394a2
```

### 客户端接入方式
建议用户使用标准版（例如 [jedis](https://intl.cloud.tencent.com/document/product/239/7043)，非 jedis cluster）的客户端访问云数据库 Redis 内存版（集群架构），这种方式接入效率更高，使用简单，同时也支持 cluster 客户端的接入，例如使用 jedis cluster。

### Codis 兼容性
腾讯云数据库 Redis 内存版（集群架构）100%兼容 Codis-server 命令，业务无需更改，通过 DTS 服务即可快速迁移数据至云数据 Redis。相对于 Codis 有如下优势：
- 兼容版本更多，Codis 已停留在3.2版本，云数据库 Redis 内存版（集群架构）现在已支持4.0、5.0版本，且后续将持续跟进社区版本更新。
- 兼容命令更多，Codis 不支持阻塞命令的执行，如 BLPOP、SUBSCRIBE 等命令。
- Codis 的数据迁移遇到大 Key 情况，可能会导致服务不可用，而云数据库 Redis 支持无损扩展，无惧大 Key。

## 兼容性检查
目前没有工具可以100%确认从标准迁移到集群是否存在兼容性问题，下文提供的2个工具可用来辅助评估兼容性，从标准迁移到集群时，建议在迁移之前做好静态评估、动态评估、业务验证3个方面的验证工作，保证迁移工作顺利进行。

### 静态评估
1. [下载 cluster_migrate_online_check.py 静态工具](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_check.py)，通过该工具执行 info commandstats 命令，分析标准版是否执行过跨 SLOT 相关命令，来辅助判断是否可能存在兼容性问题。
```
Usage：
./cluster_migrate_check.py host port password 
```
>?`host、port、password` 输入标准版 Redis 的信息。
2. 参考上文的 [兼容性说明](#jrxsm)，业务侧逐一评估每一项是否可通过。

### 动态评估
[下载 cluster_migrate_online_check 动态验证工具](https://redis-doc-2020-1254408587.cos.ap-guangzhou.myqcloud.com/cluster_migrate_online_check)，通过该工具模拟客户端执行 psync 命令，从标准版实时同步增量数据至云数据库 Redis 内存版（集群架构），通过实时同步，可以确认写入命令是否存在兼容性问题。该工具无法覆盖读命令是否兼容的测试。

动态验证步骤如下：
1. 在 [控制台](https://console.cloud.tencent.com/redis) 开通云数据库 Redis 内存版（集群架构）。
2. 通过工具从标准版实时同步数据至云数据库 Redis 内存版（集群架构）。
3. 经过一段时间的验证（如6小时或者24小时），如果工具没有报错说明写入命令没有兼容性问题，如果有报错可根据报错信息得到不兼容的命令信息。
```
Usage：
./cluster_migrate_online_check srcip:srcport srcpasswd dstip:dstport dstpasswd 
环境变量参数：
export logout=1  //打印命令到控制台，默认关闭
export pipeline = 2000  //pipeline 并发数量，默认1000
```
>?
>- `srcip:srcport`：必填，输入标准版 Redis 的地址信息。
>- `dstip:dstport`：可选，输入云数据库 Redis 内存版（集群架构）的地址信息，不填目标信息时可将该工具当 monitor 使用。
4. 参考上文的 [兼容性说明](#jrxsm)，业务侧逐一评估每一项是否可通过。

### 业务验证
为确保顺利进行迁移，建议用户在测试环境进行业务测试验证，通过将测试环境的业务连接至云数据库 Redis 内存版（集群架构），来确认每个功能无误后再进行迁移。

## 使用 DTS 进行在线迁移
迁移详细步骤请参见 [使用 DTS 进行迁移](https://intl.cloud.tencent.com/document/product/239/31941)。

## 自建实例迁移失败处理
-  client-output-buffer-limit 参数配置过小，建议该参数配置到512MB或1024MB，配置命令如下：
```
config set client-output-buffer-limit "slave 1073741824 1073741824 600"
```
- EVAL 命令未传参数。

