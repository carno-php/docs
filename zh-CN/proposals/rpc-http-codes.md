# RPC HTTP 状态码

> [draft] 为待确定提案

> 错误处理参考 > [标准错误处理流程](rpc-http-errors.md)

## 200

正常业务数据返回

## 302 [draft]

请求跳转

* 服务正在 Shutdown，不接受新请求
* 返回 Location 重复当前 URL `http://n.g.s/invoke/service`，客户端通过名称筛选其他服务节点

## 400

请求错误

* HTTP 请求不规范（RPC 下只能 POST）
* URL 不规范（路径格式 /`[invoke]`/service/method）
* Payload 解析不了
* 等等

## 404

资源未找到

* Service 不存在
* Method 不存在

## 500

系统层出错

* 框架抛出的异常
* 未捕获的业务异常
* 其他未知错误

## 503

服务不可用

> 需要保证请求还没有被处理，直接拒绝

* 服务还没有 Ready
* 服务进入限流
* 服务进入熔断
