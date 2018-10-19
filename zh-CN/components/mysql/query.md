# 数据查询

```php
// 获取一条记录
$array = yield $conn->table('table')
    ->where(['kk' => 'vv', 'kk2' => 'vv2'])
    ->where('key', 'val') // key = val
    ->where('key2', '>', 'val')
    ->where('key3', 'like', '%val%') // key expr val
    ->where('key4 <> 233') // 直接写 SQL
    ->where(123) // 主键匹配 id = 123
    ->where([['key', '<=', 'val'], ['key' => 'val'], [123]]) // 一次性提供多个 where 条件
->get();

// 获取多条记录
$arrayRows = yield $conn->table('table')
    ->select('field1', 'field2') // select 字段
    ->select('field2 as alias') // 直接写 SQL
    ->order('id', 'asc') // field, sort
    ->order('id desc') // 直接写 SQL
    ->order([['id', 'desc'], ['rank', 'asc']]) // 多个 order
    ->limit(100) // rows = limit 0, 100
    ->limit(100, 20) // offset, rows = limit 100, 20
->list();

// Where 组合
$got = yield $conn->table('table')
    ->where('id', 1)
    ->and(function (\Carno\Database\SQL\Builder $builder) {
        $builder->where('user', -1);
        $builder->where('deletedAt', '<>', 0);
    })
    ->or(function (\Carno\Database\SQL\Builder $builder) {
        $builder->where('status', 0);
        $builder->where('rank', '<', 100);
    })
->get();
// 实际执行的 SQL
// select * from table where id=1 and (user=-1 and deletedAt<>0) or (status=0 and rank < 100)
```
