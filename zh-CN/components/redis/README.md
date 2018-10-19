# Redis 的使用

## 声明对象

```php
namespace App\Redis;

use Carno\Net\Endpoint;
use Carno\Pool\Options;
use Carno\Redis\Cluster;

// 基于集群的 Redis 实现
class Storage extends Cluster
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

## 引用实例

> 参考 [依赖注入](../container/di.md)

```php
/**
 * @inject // 启用依赖注入
 * @see Storage
 * @var \Redis
 */
private $storage = null;
```
