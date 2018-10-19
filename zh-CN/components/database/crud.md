# SQL 操作

## 插入

```php
/**
 * @var \Carno\Database\Results\Created $inserted
 */
$inserted = yield $this->db->execute('insert into rooms (`name`,`owid`) values (:name,:owid)', ['name' => 'new', 'owid' => 2]);
var_dump($inserted->id()); // 新插入的 Row ID
```

## 查询

```php
/**
 * @var \Carno\Database\Results\Selected $rooms
 */
// 查询不带条件
$rooms = yield $this->db->execute('select id from rooms');
// 查询带条件
$rooms = yield $this->db->execute('select * from rooms where id = 1');
// 使用参数绑定，格式只能使用 ":key" 或者 "?id"
$rooms = yield $this->db->execute('select * from rooms where id = :id', ['id' => 123]);
var_dump($rooms);
```

## 更新

```php
/**
 * @var \Carno\Database\Results\Updated $updated
 */
$updated = yield $this->db->execute('update rooms set name=:name where id=:id', ['name' => 'new', 'id' => 1]);
var_dump($updated->rows()); // 更新的行数
```

## 删除

```php
/**
 * @var \Carno\Database\Results\Updated $deleted
 */
$deleted = yield $this->db->execute('delete from rooms where id=:id', ['id' => 1]);
var_dump($deleted->rows()); // 删除的行数
```

> 为了通过 IDE 对 SQL 的语法检查，建议 SQL 表达式中使用 ":string" 或者 "?int" 的写法
> 例如
> `SELECT * FROM users WHERE id = :id`
> `UPDATE users SET name = ?0 WHERE id=?1 LIMIT 1"`
