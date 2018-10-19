# 客户端方法

> [使用长连接](pool-ka.md)

## 发送请求

### GET

```php
// 可选自定义参数
$options = (new \Carno\HTTP\Options)->setTimeouts(3500);
// $options 为可选参数
$resp = yield \Carno\HTTP\Client::get('http://httpbin.org/get', ['X-Extra-Header' => 'value'], $options);
```

### POST

#### 自定义 payload

```php
$resp = yield \Carno\HTTP\Client::post('http://httpbin.org/post', 'some-data', ['Content-type' => 'text/plain']);
```

#### POST 数组

```php
// Content-type 指定为 application/json 会自动 json_encode
$resp = yield \Carno\HTTP\Client::post('http://httpbin.org/post', ['key' => 'v'], ['Content-type' => 'application/json']);
```

#### POST 表单

```php
// 不指定 Content-type 的情况下会自动使用表单方式提交
$resp = yield \Carno\HTTP\Client::post('http://httpbin.org/post', ['field' => 'v']);
```

> [文件上传](uploading.md)

### DELETE

```php
$resp = yield \Carno\HTTP\Client::delete('http://httpbin.org/delete');
```

### UPGRADE

> [WebSocket 握手](ws-upgrade.md)

## 响应处理

上述接口的返回值是 `Carno\HTTP\Client\Responding` 对象

### 获取响应信息

```php
$resp->code(); // 返回 HTTP 状态码
$resp->phrase(); // 返回状态说明（200 = "OK", 404 = "Not Found"）
$resp->header('key'); // 获取返回 header 值（不存在时返回 null）
```

### 获取响应数据

> 不对 HTTP 状态判断

```php
$resp->payload(); // 获取任意内容
```

> 判断 HTTP 状态（4xx 或者 5xx 时抛出异常 `Carno\HTTP\Exception\ErrorResponseException`）

```php
$resp->data(); // 获取成功内容
```
