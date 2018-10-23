# Protobuf 设计规范

## 协议版本

proto3

## 名词定义

* package > 等同于命名空间
* message > proto 里的结构体，用于 RPC 的 Request/Response 参数描述和实体定义
* service > proto 里的服务定义
* rpc > Service 里的接口定义

## 命名约定

> 大驼峰法是首字母大写的驼峰，例如：HelloWorld
>
> 小驼峰法是首字母小写的驼峰，例如：helloWorld

1. package 使用三段以点分隔（`namespace.group.server`）
    * 各段使用 **小驼峰法** 命名；例如：biz.foo.bar
2. message 和 service 名称使用 **大驼峰法**；例如：AccessInfo
3. message 结构字段和 rpc 使用 **小驼峰法**；例如：appId, getUser
4. enum 约定
    * 命令使用 **大驼峰法**；例如：Errors
    * 键使用 **全大写**，多个单词使用 **下划线** 分隔；例如：FOO_BAR

## 设计规范

### 命名规则

1. service 使用 **名词** 方式，且尽量只使用一个单词
2. rpc 的 Request/Response 都必须是单独的 message（不允许共用）
    > 格式为 `(service)(rpc)[Request/Response]`
    ```proto
    // demo
    service User {
       rpc getInfo(UserGetInfoRequest) returns (UserGetInfoResponse);
    }
    ```
3. rpc 使用 **动词** / **动词+名词** 方式
    > 正确的格式：invoke, getUser, blockUser
    >
    > 错误的格式：info, dataChange, userData
4. service + rpc 不应该出现重复的单词
    > 例如 User.getUserInfo 应该改成 User.getInfo
5. message 最好只使用 **名词** 表示（Request/Response 除外）

### Service 设计

1. rpc 的 Request/Response 可以允许空结构（不包含任何字段），比如接口不需要任何输入和返回
2. 一个 proto 文件内 **只能** 存在一个 service，多个需要拆分到不同的 proto 文件中
    > 建议 service 的名称和 proto 文件名保持一致；
    >
    > 例如：`search.proto` 里只有一个 `service Search`
3. 不同 service 共用的 message 使用单独文件放置，比如放在 `your/entity/some.proto`

### 错误代码

1. 业务上的错误代码需要通过 enum 来定义
2. 一个 package 下应该只包含一个错误代码的 enum 且放置在 errors.proto 文件中
    > 名称建议使用 **Errors**
    ```proto
    package ns.g.s;
    enum Errors {
        SYSTEM_BUSYING = 10001;
        ACCESS_DENIED = 20001;
        GRANT_EXPIRED = 30001;
    }
    ```
3. 此处的 enum 需要符合标准的命名规范

## 书写规范

* 缩进：__4__ 个空格

### proto 文件头

```proto
syntax = "proto3";

package namespace.group.server;

import "ns.g.s/entity/struct.proto"
```

### message 样例

```proto
message Request {
    string query = 1; // 对于 "query" 字段的注释
    int32 number = 2;
    int32 page = 3;
}
```

### service 样例

```proto
service Search {
    // "invoke" 接口的注释
    rpc invoke (Request) returns (Response);
    rpc method (Request) returns (Response);
}
```
