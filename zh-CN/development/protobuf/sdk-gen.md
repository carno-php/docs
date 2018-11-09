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

```sh
docker run --rm -it -v $(pwd):/protobufs carno/protoc-gen OUTPUT INPUT
```

1. OUTPUT 为 SDK 的输出目录，不存在时会自动创建（路径需要先挂载到容器中）
2. INPUT 为需要编译的文件或者目录，指定目录时会遍历目录下所有的 .proto 文件并编译
