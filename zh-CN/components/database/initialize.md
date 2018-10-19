# 创建数据库实例

## 使用 MySQL

### 声明对象

```php
namespace App\Databases;

use Carno\Database\Clusters\MySQL;
use Carno\Net\Endpoint;
use Carno\Pool\Options;

// 基于集群的 MySQL 实现
class Goods extends MySQL
{
    protected $server = 'storage'; // 申请到的 Server 名

    /**
     * 指定连接池的配置参数（可以按照连接的 endpoint 分别配置）
     */
    protected function options(Endpoint $endpoint) : Options
    {
        return new Options;
    }
}
```

### 引用实例

> 参考 [依赖注入](../container/di.md)

```php
/**
 * @inject // 启用依赖注入
 * @var \App\Databases\Goods
 */
private $storage = null;
```
