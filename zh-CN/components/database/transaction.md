# 事务操作

```php
try {
    $finished = yield $db->transaction(function (\Carno\Database\Programs\Transaction $trans) use ($db) {
        /**
         * @var \Carno\Database\Results\Created $r
         */
        // 直接执行 SQL 的话必须使用 $trans 提供的 execute 方法
        $r = yield $trans->execute('insert into rooms (`name`) values (:name)', ['name' => 'new']);
        var_dump('[1] new id is '.$r->id());

        // 使用 SQLBuilder，table 的第二个参数必须要传，否则会出错
        $id = yield $db->table('rooms', $trans->link())->insert(['name' => 'new']);
        var_dump('[2] new id is '.$id);

        if ('your-condition') {
            // yield $trans->rollback(); // 手动回滚
            throw new Exception('automatic rollback'); // 抛出任意异常时会自动回滚
        }

        // yield $trans->commit(); // 手动提交

        return 'ok'; // 函数执行完时会自动提交，这里也可以不写 return
    });
    var_dump($finished); // 输出 "ok" - 函数的 return 值
} catch (Throwable $e) {
    dump($e);
}
```
