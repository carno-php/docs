# 生成 SDK

示例文件：hello.proto

```proto
syntax = "proto3";

package carno.tests.hello;

message Payload {
    string data = 1;
}

service Hello {
    rpc world(Payload) returns (Payload);
}
```

## 安装 protoc-gen

> 首先请安装 protoc <https://github.com/protocolbuffers/protobuf>

然后在命令行下执行（需要先安装 golang）

```sh
go get -u github.com/carno-php/protoc-gen
```

### 生成代码（PHP）

```sh
protoc --plugin=protoc-gen-custom=$(which protoc-gen) --custom_out=. hello.proto
```

> 生成后的代码示例 <https://github.com/carno-php/protoc-hello>

## 使用 Docker

> TODO
