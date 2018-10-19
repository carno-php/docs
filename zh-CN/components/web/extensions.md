# 控制器扩展

extensions 提供了对请求的 输入、输出、异常 时的行为处理和拦截，可以实现下面的功能：

1. 前置校验：登录验证等
2. 全局的格式化输出
3. 异常捕获、记录和自定义输出

## 在控制器中使用扩展

> 实现了 `Extensional` 接口即可启用扩展

```php
namespace App\Controllers;

use Carno\Web\Contracts\Controller\Extensional;
use Carno\Web\Contracts\Controller\Extensions;
use Carno\Web\Controller\Based;

class Hello extends Based implements Extensional
{
    /**
     * @var Extensions
     */
    private $ext = null;

    /**
     * @return Extensions
     */
    public function extension() : Extensions
    {
        return $this->ext ?? $this->ext = new YourExtHandler;
    }
}
```

## 实现一个扩展 Handler

```php
namespace App\Library;

use Carno\HTTP\Standard\Response;
use Carno\Web\Contracts\Controller\Extensions;
use Carno\Web\Controller\Based;
use Throwable;

class Handler implements Extensions
{
    /**
     * @param Based $session
     * @return Response|null
     */
    public function requesting(Based $session) : ?Response
    {
        // 返回 Response 对象会直接结束 action 的执行并返回指定的 Response

        // $session 是 controller 实例

        // 可以直接使用 controller 提供的 base 方法
        return $session->redirect('/user/login');
        return $session->response('some data');

        // 这里设置的上下文，可以在 controller 的 action 中拿到
        $session->ctx()->set('key', 'val');

        // 自定义 Response 返回
        return new Response(502);

        // 和 action 的执行在同一个协程内
        return yield $rpc->call();

        // 返回 null 值表示跳过拦截，继续回到 controller 执行
        return null;
    }

    /**
     * @param Based $session
     * @param mixed $result
     * @return Response|null
     */
    public function responding(Based $session, $result) : ?Response
    {
        // 和 requesting 的使用方式一致
        // $result 是 action 执行后返回的值
        // 可以自行处理后通过 Response 返回
        return $session->response('new data');

        // 跳过处理，后面会走标准的 action 返回值处理流程
        return null;
    }

    /**
     * @param Based $session
     * @param Throwable $e
     * @return Response|null
     */
    public function exceptions(Based $session, Throwable $e) : ?Response
    {
        // 和 requesting 的使用方式一致
        // $e 是 action 执行过程中抛出的异常

        // 这里返回 Response 会吞掉异常，不抛出，走标准的返回流程

        return new Response(500, [], 'some error');

        // 返回 null 会抛出异常，走默认的异常处理流程
        return null;
    }
}
```
