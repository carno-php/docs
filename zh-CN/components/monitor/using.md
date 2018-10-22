# 业务接入

> Metrics::func() 会返回一个新的监控指标，请保证全局单例

## 方法 1 （直接创建）

直接在 Service 的 __construct 中创建

```php
class Service implements API
{
    private $counter = null;

    public function __construct()
    {
        $this->counter = Metrics::counter()->named('metric');
    }

    public function func()
    {
        $this->counter->inc(100);
    }
}
```

## 方法 2 （DI 注入 LIB）

创建 library，然后在 Service 里使用 DI 注入

.. 创建 library

```php
class Lib
{
    private $m1 = null;

    public function __construct()
    {
        $this->m1 = Metrics::counter()->named('metric');
    }

    public function m1()
    {
        return $this->m1;
    }
}
```

.. 在业务 Service 中使用 DI 注入

```php
class Service implements API
{
    /**
     * @inject
     * @var Lib
     */
    private $metrics = null;

    public function func()
    {
        $this->metrics->m1()->inc(100);
    }
}
```
