# 引用 SQL Builder

首先 [创建一个数据库实例](../database/initialize.md)

然后在实例中通过 `use` 的方式载入 `trait`

```php
use Carno\Database\SQL\Kit;

class Goods extends MySQL
{
    use Kit;
}
```
