# 支持的缓存方式

## 基于网络

> 目前暂时只支持基于 Redis 的实现

首先 [创建一个 Redis 实现](../redis/README.md)

创建缓存对象

```php
namespace App\Caches;

use App\Redis\HAInstance;
use Carno\Cache\Adaptors\Network;

class User extends Network
{
    /**
     * @inject
     * @var HAInstance
     */
    private $redis = null;

    /**
     * 指定网络驱动实例
     */
    protected function driver() : object
    {
        return $this->redis;
    }
}

```

## 基于内存

> 默认使用 APCu，没有安装扩展或者未启用的情况下会自动切换 PHP 本地实现（均支持 TTL）

创建缓存对象

```php
namespace App\Caches;

use Carno\Cache\Adaptors\Memory;

class Token extends Memory
{

}
```
