# HTTP 路由

## 路由描述

路由描述类的加载在 APP 根目录下的 `routes.php` 中

routes.php 示例

```php
return [
    \App\Routers\Endpoint::class, // 指定路由描述文件
    // 可以加载多个 class
];
```

## 路由规则

> URL 的书写规则参见 <https://github.com/nikic/FastRoute>

```php
namespace App\Routers;

use App\Controllers\Hello;
use Carno\Web\Controller\Based;
use Carno\Web\Router\Configure;
use Carno\Web\Router\Setup;

class Endpoint extends Configure
{
    /**
     * 在路由里把需要使用的 controller 通过 DI 的方式引入进来
     * @inject
     * @var Hello
     */
    private $hello = null;

    /**
     * 所有访问修饰符为 "protected" 且参数只有一个 "Setup" 的方法会被路由配置程序执行
     * @param Setup $setup
     */
    protected function route1(Setup $setup) : void
    {
        // "/hello-world" 的 GET 请求会被转到 "Hello" 的 "world" 方法中
        $setup->get('/hello-world', [$this->hello, 'world']);

        // POST 请求
        $setup->post('/hello-world', [$this->hello, 'world']);

        // 其他支持的单个 HTTP method
        $setup->head();
        $setup->options();
        $setup->put();
        $setup->patch();
        $setup->delete();

        // 允许多种 HTTP method
        $setup->match(['options', 'get', 'post'], '/multi-method', [$this->hello, 'methods']);

        // RESTFul 请求，会映射 "post,get,put,patch,delete" 5种方法，controller 中要有对应的实现（名称一致）
        $setup->rest('/rest-api', $this->hello);

        // 允许所有的 method (options,head + post,get,put,patch,delete)
        $setup->any('/any-method', [$this->hello, 'methods');
    }

    /**
     * 这个也会被执行
     * @param Setup $setup
     */
    protected function route2(Setup $setup) : void
    {
        // 创建基于 prefix 的组，命名为 user
        $user = $setup->group('/user', 'user');

        // 实际访问路径为 /user/info
        $user->get('/info', [$this->hello, 'user']);

        // 继续添加
        $user->post();

        // 再创建一个 group
        $admin = $setup->group('/admin', 'admin');
        $admin->get('/dashboard', [$this->hello, 'admin']);
    }

    /**
     * @param Setup $setup
     */
    protected function route3(Setup $setup) : void
    {
        // 简单的匿名函数处理
        $setup->get('/', function (Based $session) {
            return 'Hi';
        });

        // 自定义 class 的回调（非 controller）
        $custom = new class {
            public function publicInfo(Based $session)
            {
                return $session
                    ->response(json_encode(['hi' => 'moyo']))
                    ->withHeader('Content-type', 'application/json')
                ;
            }
        };

        $setup->get('/public', [$custom, 'publicInfo']);
    }

    /**
     * 这个不会被主动执行
     */
    private function test1() : void
    {

    }
}
```
