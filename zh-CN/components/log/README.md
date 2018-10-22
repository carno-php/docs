# 日志输出

## 使用示例

```php
// 可选日志等级 emergency/alert/critical/error/warning/notice/info/debug
logger('cluster')->info('Service watcher has been closed', ['name' => $name]);
```

* logger(`SCENE`) 参数为场景名称，不同的场景可以通过配置中心设定不同的日志等级和输出地址
* 场景名为可选值，默认为 `default`，不知道用什么的情况下可以不传
* 场景名为全局资源，自定义时应该避免冲突
