# 目录

## 基础信息

* [运行](runtime/README.md)
  * [环境依赖](runtime/env.md)

## 组件列表

* 实例管理
  * [依赖注入](components/container/di.md)
* HTTP 服务端
  * [上手](components/web/quickstart.md)
  * [路由](components/web/router.md)
  * [控制器](components/web/controller.md)
  * [扩展](components/web/extensions.md)
* HTTP 客户端
  * [命令支持](components/http/client/methods.md)
  * [文件上传](components/http/client/uploading.md)
  * [自动连接池](components/http/client/pool-ka.md)
  * [WS Upgrade](components/http/client/ws-upgrade.md)
* [Redis](components/redis/README.md)
* [缓存](components/cache/README.md)
  * [存储方式](components/cache/drivers.md)
  * [自动刷新](components/cache/delegate.md)
* 数据库
  * [创建实例](components/database/initialize.md)
  * [执行SQL](components/database/crud.md)
  * [事务操作](components/database/transaction.md)
  * SQL Builder
    * [查询](components/mysql/query.md)
    * [计算](components/mysql/calc.md)
    * [汇聚](components/mysql/merge.md)
    * [更新](components/mysql/update.md)
    * [分页](components/mysql/paginator.md)
    * 扩展
      * [自动时间戳](components/mysql/features/timestamps.md)
* 消息队列
  * [NSQ](components/nsq/README.md)
    * [集群模式](components/nsq/cluster.md)
* [配置中心](components/config/README.md)
  * [加载方式](components/config/loaders.md)
  * [变化通知](components/config/watching.md)
  * [对象绑定](components/config/bind.md)
* [日志输出](components/log/README.md)
  * [动态配置](components/log/config.md)
  * 日志复制
    * [Log.IO](components/log/replicas/logio.md)

## 设计规范

* 业务实现
  * [Protobuf](standards/protobuf.md)
* 协议规范
  * [RPC HTTP codes](proposals/rpc-http-codes.md)
  * [RPC HTTP 错误处理](proposals/rpc-http-errors.md)
