# 数据更新

```php
// 更新记录
$affectRows = yield $conn->table('table')
    ->where('id', 123)
    ->data(['f1' => 'val', 'f2' => 'val'])
    ->data('`f3` = CONCAT(`f1`, `f2`)') // 直接写 SQL
    ->update(['f1' => 'val']) // 也可以省略前面的 data 直接把数据写在 update 参数中
;

// 插入记录
$insetID = yield $conn->table('table')
    ->data(['f1' => 'val'])
    ->insert(['f2' => 'val']) // 也可以省略前面的 data 直接把数据写在 insert 参数中
;

// 删除记录
$affectRows = yield $conn->table('table')
    ->where('id', 222) // 删除条件
    ->limit(1) // 限制条数
    ->delete('id2', 333) // 也可以直接把 where 条件写在 delete 参数中
;
```
