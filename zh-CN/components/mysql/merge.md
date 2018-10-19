# 数据汇聚

```php
// 关联数据（行内 merge）（单条）
$related = yield $conn->table('table')
    ->relation('table2', 'bind', 'id', function (\Carno\Database\SQL\Builder $builder) {
        // select * from table2 where bind in (1,2,3) and status = 1
        $builder->where('status', 1);
    })
->get(); // 得到 table 和 table2 合并的数据

// 关联数据（行内 attach）(多条)
$related = yield $conn->table('table')
    ->relations('table2', 'bind', 'attached', 'id')
->get(); // 返回数据包含 attached 字段，内容是 table2 的关联内容
```
