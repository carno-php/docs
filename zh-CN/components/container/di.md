# 依赖注入

> 直接通过 new 创建的实例不会执行依赖注入（请使用 Carno\Container\DI::object 来创建实例）

## 实现自动注入

### 1. 通过 property 注解

```php
namespace Demo;

use My\Library;
use My\Lib2;
use My\TypeHint;

class SomeService
{
    /**
     * !!这里必须包含 @inject 和 @var 标签
     * 通过 @injec 注解告诉框架这个 property 需要注入实例
     * @inject
     * 注入的实例 class 是 My\Library （默认注入的是单例）
     * @var Library
     */
    private $library = null;

    /**
     * @inject
     * !!这里实际注入的是 My\Lib2 的实例（因为有 "@see Lib2"，"@var TypeHint" 只是为了 IDE 的自动提示）
     * @see Lib2
     * @var TypeHint
     */
    private $lib2 = null;

    public function test()
    {
        // 这里就可以直接调用了
        var_dump($this->library->invoke());
    }
}
```

### 2. 通过 __construct 构造函数

```php
namespace Demo;

use My\Library;

class SomeService
{
    /**
     * 这里注释可以随便写
     */
    private $library = null;

    public function __construct(Library $library)
    {
        // 传入的 $library 是已经实例化过的 My\Library::class（单例）
        $this->library = $library;
    }

    public function test()
    {
        // 这里就可以直接调用了
        var_dump($this->library->invoke());
    }
}
```
