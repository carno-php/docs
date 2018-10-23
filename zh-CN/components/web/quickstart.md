# 快速上手

> [环境依赖](../../runtime/env.md)

## 使用 composer 来创建应用

```sh
composer create-project carno-php/skel-httpd my-web-server
```

> 国内加速 <https://packagist.laravel-china.org>

## 启动应用

先进入到 `my-web-server` 目录，然后执行

```sh
./vendor/bin/httpd server:start --listen=:8080 --debug
```

通过 curl 访问

```sh
curl http://127.0.0.1:8080/
```

或者打开浏览器访问 <http://127.0.0.1:8080/>
