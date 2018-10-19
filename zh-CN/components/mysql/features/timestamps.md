# 自动时间戳

> 首先需要在数据库对象里添加 Trait `use Carno\Database\SQL\Features\Timestamps;`
> 默认创建时间字段为 **createdAt** 修改时间字段为 **updatedAt** （可以重载对象属性字段来自定义）

示例代码

```php
// 数据库对象
class Crawler extends MySQL
{
    use \Carno\Database\SQL\Features\Timestamps;
    protected $server = 'local-test';
    protected $createdAt = 'Your created timestamp field';
    protected $updatedAt = 'Your updated timestamp field';
}
```

使用上和一般的更新操作一致，只是数据表的字段会自动填充并更新
