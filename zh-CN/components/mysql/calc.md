# 数据计算

```php
// 查询是否存在，参数和 where 的使用方式一致
$bool = yield $conn->table('table')->exists('key', 'val');

// count
$count1 = yield $conn->table('table')->count();
$count1 = yield $conn->table('table')->count('DISTINCT channel');

// sum
$sum = yield $conn->table('table')->sum('field');

// max
$max = yield $conn->table('table')->max('field');

// min
$min = yield $conn->table('table')->min('field');

// avg
$avg = yield $conn->table('table')->avg('field');
```
