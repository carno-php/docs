# 配置中心

## 读取示例

```php
// config 为内存操作，不需要加 yield 关键字
if (config()->has('some-key')) {
    // 原始格式
    $raw = config()->get('some-key');
    // 获取 int 类型
    $int = config()->int('some-key');
    // 获取 string 类型
    $str = config()->string('some-key');
}
```

## 资源分配

1. config() 默认参数是指向自己的服务 `namespace.group.server` （一般情况下 config 使用时不要加任何参数）
2. 框架默认会使 `ns.g.s` 跟随 `global`，作为一种上下游同步机制，实现的效果为服务配置里没有的数据会自动查找 `global` 下的同名配置

> `global` 机制主要解决了服务数量庞大的场景下，需要全局统一配置又需要按服务定制配置的需求
