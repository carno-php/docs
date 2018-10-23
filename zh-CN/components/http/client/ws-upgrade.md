# WebSocket 握手

## Upgrade

```php
$framed = yield Client::upgrade('wss://echo.websocket.org');
```

$framed 的类型是 `Carno\HTTP\Client\Framing`

支持的操作方法

1. ->socket() - 对 Socket 的直接操作
2. ->message() - 数据帧接收

## Framed

### Socket

方法列表

- valid - 检查连接是否有效（有没有被关闭）
- push(Frame) - 推送数据帧
- close() - 关闭 Socket 连接

### Message

返回 Channel 对象，参考 [Channel 使用说明](../../channel/usages.md)
