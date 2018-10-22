# 变化通知

```php
// watch 某个 key 的变化，键值存在时会立即触发回调，后面有变化时会继续触发回调
config()->watching('some-key-to-watch', function ($value) {
    var_dump('new value is '.$value);
});
```

> key 被删掉的时候回调参数 $value 值为 null
