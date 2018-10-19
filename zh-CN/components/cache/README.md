# 缓存

> 使用缓存组件而不是直接使用 Redis 之类的原因是为了约束使用习惯，防止滥用，并方便以后更换其他缓存实现

## 使用示例

```php
if (yield $this->cache->has('some-key')) {
    $dat = yield $this->cache->read('some-key');
} else {
    $dat = 'some data from backend';
    yield $this->cache->write('some-key', $dat, 30);
}
var_dump($dat);
```
