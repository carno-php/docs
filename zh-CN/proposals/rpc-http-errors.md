# RPC HTTP 错误处理

## 标准错误处理流程

### HTTP header 定义

* X-Err-Code 错误代码，类型 **int**
* X-Err-Message 错误信息，类型 **string**

1. HTTP 200 情况下
   * 一定会有 **X-Err-Code**
   * 可能会有 X-Err-Message
   * X-Err-Message 可能是空字符串
2. HTTP 500 情况下
   * 可能会有 X-Err-Code
   * 可能会有 X-Err-Message

### HTTP body 定义

> 在遵循上述 HTTP header 规则的前提下，body 里会包含一份用 JSON 描述的错误信息

JSON 字段映射：

```text
X-Err-Code --> code
X-Err-Message -> message
```

> JSON 数据完全是 header 数据的 copy，header 里没有的字段 JSON 里也不会出现

### 错误处理代码

```php
// 通过 headers 判断

if http.code == 200 {
  if http.headers.has('X-Err-Code') {
    code = http.headers.get('X-Err-Code')
    message = http.headers.get('X-Err-Message') ?: "Default error message"
    // 业务错误
  } else {
    // 成功请求
  }
} elseif http.code == 500 {
  code = http.headers.get('X-Err-Code') ?: 10000
  message = http.headers.get('X-Err-Message') ?: "Default error message"
  // 系统错误
}

// 通过 json 判断

if http.code == 200 {
  if http.headers.has('X-Err-Code') {
    json = http.body.decode
    code = json.get('code')
    message = json.get('message') ?: "Default error message"
    // 业务错误
  } else {
    // 成功请求
  }
} elseif http.code == 500 {
  json = http.body.decode
  code = json.get('code') ?: 10000
  message = json.get('message') ?: "Default error message"
}
```
