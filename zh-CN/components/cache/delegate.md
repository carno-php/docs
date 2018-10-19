# 自动刷新

## 使用示例

```php
$data = yield $this->cache->delegate('some-key', function () {
    return yield \Carno\HTTP\Client::get('http://www.baidu.com/');
}, 30); // 每隔30秒主动进行刷新
var_dump($data);
```

说明：

1. 缓存不存在时会直接执行 $getter 函数来刷新数据（目前策略）
