# 控制器

## 使用示例

```php
namespace App\Controllers;

use Carno\HTTP\Standard\Response;
use Carno\Web\Controller\Based;

class Hello extends Based
{
    public function world()
    {
        // 操作上下文
        // 等同于 yield ctx();
        $this->ctx();

        // 获取请求的 action 信息，当前为 "world"
        $this->request()->action();

        // 获取请求的原始 payload 数据
        // 例如 content-type 为 application/json 时直接拿到 json 原始内容
        $this->request()->payload();

        // 获取请求 GET 数据
        $this->request()->get();

        // 获取请求 POST 数据（form 表单）
        // 请求 content-type 为 application/json 时，此处为 json 的解析后数据
        $this->request()->post();

        // 获取 cookies 数据
        $this->request()->cookies();

        // 获取路由的 params 信息
        // 例如 "/user/{id:\d+}" 可以拿到 id 的值
        $this->request()->params();

        // 获取 get/post/cookies 混合数据（等同 PHP 的 $_REQUEST）
        $this->request()->mixed();

        // 上述 get/post/cookies/params/mixed 的返回值是 VGetter 对象

        // 支持转成数组
        $data = (array) $this->request()->get();

        // 直接通过 key 访问数据
        $this->request()->get()->key;

        // 类型转为 string，默认值 default
        $this->request()->get()->string('key', 'default');

        // 类型转为 int，默认值 123
        $this->request()->post()->integer('int', 123);

        // 类型转为 bool，默认值 true
        // 输入 "true", "yes" 时返回 true，"false", "no" 时返回 false
        $this->request()->post()->boolean('bool', true);
    }

    public function result()
    {
        if ($this->request()->cookies()->boolean('redirect')) {
            // 默认 302 跳转
            return $this->redirect('http://example.com');
            // 指定 301 跳转 $permanently
            return $this->redirect('http://httpbin.org', true);
        }

        // 直接返回 Response 对象
        if (2) {
            // 指定内容
            return $this->response('hello');
            // 指定返回 code
            return $this->response()->withStatus(500);
        }

        // 设置头，会在返回时生效
        $this->response()->withHeader('Content-type', 'application/json');

        if (3) {
            // 通过 response 设置返回内容
            $this->response('{}');
            return;
        }

        if (4) {
            // 直接返回内容
            return '{}';
        }
    }

    public function resp()
    {
        // 支持的返回格式

        // 直接返回 string
        return '{}';

        // 返回数组
        // 会根据请求 Accept 类型自动编码，默认 json
        return ['aa' => 'bb'];

        // 返回对象

        // 支持 Carno\HTTP\Standard\Response 标准返回
        return new Response(502);

        // 支持 ArrayObject，会转成数组后再按照标准流程输出
        return new \ArrayObject([1, 2, 3]);

        // 支持 protobuf message，会强制输出为 json
        return new \Google\Protobuf\Internal\Message;

        // 支持存在 __toString 方法的对象输出
        return new class {
            public function __toString()
            {
                return 'hello';
            }
        };
    }
}
```
