# 快速上手

> 服务的实现依赖 Protobuf SDK，查看 [SDK 生成器](../../development/protobuf/sdk-gen.md)

## 使用 composer 来创建应用

```sh
composer create-project carno-php/skel-rpcd my-service
```

> 国内加速 <https://packagist.laravel-china.org>

## 引用 SDK

> 测试时可以使用 demo SDK `carno-php/protoc-hello`

执行

```sh
composer require your/sdk
```

## 实现服务

在 `src/Services` 目录下实现 SDK 中约定的 `Contracts`

例如：Hello.php

```php
namespace App\Services;

use Carno\RPC\Server;
use Carno\Tests\Hello\Payload;

class Hello extends Server implements \Carno\Tests\Hello\Contracts\Hello
{
    /**
     * @param Payload $request
     * @return Payload
     */
    public function world(Payload $request)
    {
        return $request;
    }
}
```

## 注册服务

在 `APP` 根目录下的 `registers.php` 里添加

```php
return [
    \App\Services\Hello::class,
];
```

## 启动服务

先进入到 `my-service` 目录，然后执行

```sh
./vendor/bin/rpcd server:start --listen=:8080 --debug
```

通过 curl 测试

```sh
curl -v -d '{"data":"hello world"}' -H 'Content-type: application/json' http://127.0.0.1:8080/invoke/hello/world
```
