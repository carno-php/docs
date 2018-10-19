# 目录

## 基础信息

* [运行](runtime/README.md)
  * [环境依赖](runtime/env.md)

## 组件列表

* [实例管理](components/container/README.md)
  * [依赖注入](components/container/di.md)
* [Web Server](components/web/README.md)
  * [上手](components/web/quickstart.md)
  * [路由](components/web/router.md)
  * [控制器](components/web/controller.md)
  * [扩展](components/web/extensions.md)
* [Redis](components/redis/README.md)
* [缓存](components/cache/README.md)
  * [后端驱动](components/cache/drivers.md)
  * [自动刷新](components/cache/delegate.md)
* [数据库](components/database/README.md)
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

## 设计规范

* 业务实现
  * [Protobuf](standards/protobuf.md)
* 协议规范
  * [RPC HTTP codes](proposals/rpc-http-codes.md)
  * [RPC HTTP 错误处理](proposals/rpc-http-errors.md)
