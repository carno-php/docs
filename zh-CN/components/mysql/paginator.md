# 分页器

使用方式

```php
// 手动指定分页参数
// $page 是当前页数，$size 是每页大小
$result = yield $conn->table('table')->where('country', 'cn')->paged($page, $size);

// 从 pb 对象中自动配置参数
$pb = new PBInput;
$result = yield $conn->table('table')->paged($pb);

// 分页信息导出到 pb 对象

$pb = new PBOutput;
$pb = $result->export($pb);
```

paged 自动分配参数需要 PB 中必须包含 page 字段，可选 size 字段，例如下面这个结构：

```proto
message PBInput {
    int32 page = 1;
    int32 size = 2;
}
```

paged 返回值 $result 是 Carno\Database\SQL\Paginator\Pagination 对象，包含以下方法：

* total 总数据量 int
* size 分页大小 int
* prev 上一页 int
* page 当前页 int
* next 下一页 int
* last 最后一页 int
* items 当前页的数据 array
* export 页信息导出到 PB

export 导出信息时需要 PB 中包含以下字段（均可选，缺失的字段会自动跳过）

```proto
message PBOutput {
    int32 total = 1;
    int32 size = 2;
    int32 prev = 3;
    int32 page = 4;
    int32 next = 5;
    int32 last = 6;
}
```
