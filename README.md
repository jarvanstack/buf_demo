## buf_demo 

a demo of how to use buf generate protocol buffer file to golang .

> NOTE:  you need to do this on Linux, Window not support NOW!
> OFFICE DOC:https://docs.buf.build/


## QUICK START

### 1. install

> There are three ways to install buf 
> 1. bin
> 2. tar package
> 3. go/bin
> 
> we use the first bin way, you can also use other method( see doc:https://docs.buf.build/)


run command:

```shell
BIN="/usr/local/bin" && \
VERSION="0.43.2" && \
BINARY_NAME="buf" && \
  curl -sSL \
    "https://github.com/bufbuild/buf/releases/download/v${VERSION}/${BINARY_NAME}-$(uname -s)-$(uname -m)" \
    -o "${BIN}/${BINARY_NAME}" && \
  chmod +x "${BIN}/${BINARY_NAME}"
```

you can check weather you are installed success.

```bash
[root@c03 buf_demo]# buf --version
0.43.2
```

### 2. proto file

create a new folder `demo` and create a file `echo.proto`

```protobuf
syntax = "proto3";
package gateway_5;
option go_package = "gateway_5/";

message StringMessage {
  string value = 1;
}

service YourService {
  rpc Echo(StringMessage) returns (StringMessage) {}
}
```

### 3. buf.gen.yaml file

create a new file in demo folder `buf.gen.yaml`

```yaml
version: v1beta1
plugins:
  - name: go
    out: ./
    opt:
      - paths=source_relative
  - name: go-grpc
    out: ./
    opt:
      - paths=source_relative

```

### generate code

```bash
cd demo
#generate code
buf generate
```

you can see
```shell
[root@c03 buf_demo]# cd demo/
[root@c03 demo]# buf generate
[root@c03 demo]# ls
buf.gen.yaml  echo_grpc.pb.go  echo.pb.go  echo.proto
[root@c03 demo]# 

```