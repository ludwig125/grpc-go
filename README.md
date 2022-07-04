install

https://grpc.io/docs/protoc-installation/

```
$sudo apt install -y protobuf-compiler

$protoc --version  # Ensure compiler version is 3+
libprotoc 3.6.1
```

# tutorial go

https://grpc.io/docs/languages/go/quickstart/

```
git clone -b v1.46.0 --depth 1 https://github.com/grpc/grpc-go
```

この helloworld を使う

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_server/main.go
2022/07/02 06:55:00 server listening at [::]:50051
2022/07/02 06:55:07 Received: world

```

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go
2022/07/02 06:55:07 Greeting: Hello world
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $
```

https://grpc.io/docs/languages/go/quickstart/#update-the-grpc-service
に従って、proto ファイルを修正

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    helloworld/helloworld.proto
```

server と client の import 先を自分のディレクトリに修正

```go
	// pb "google.golang.org/grpc/examples/helloworld/helloworld"
	pb "github.com/ludwig125/grpc-go/helloworld/helloworld"
```

server

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_server/main.go
2022/07/02 07:07:09 server listening at [::]:50051
2022/07/02 07:07:13 Received: world
```

client

```
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go
2022/07/02 07:07:13 Greeting: Hello world
2022/07/02 07:07:13 Greeting: Hello again world
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $

[~/go/src/github.com/ludwig125/grpc-go/helloworld] $go run greeter_client/main.go --name=Alice
2022/07/02 07:09:17 Greeting: Hello Alice
2022/07/02 07:09:17 Greeting: Hello again Alice
[~/go/src/github.com/ludwig125/grpc-go/helloworld] $
```

# official tutorial

https://grpc.io/docs/languages/go/basics/

https://github.com/grpc/grpc-go/tree/master/examples/route_guide
をローカルにコピー

```
[~/go/src/github.com/ludwig125/grpc-go/route_guide] $ protoc --go_out=. --go_opt=paths=source_relative \
    --go-grpc_out=. --go-grpc_opt=paths=source_relative \
    routeguide/route_guide.proto
```

# sample

https://developers.google.com/protocol-buffers/docs/gotutorial

protoc

- ref: https://zenn.dev/hsaki/books/golang-grpc-starting/viewer/codegenerate
- https://grpc.io/docs/languages/go/quickstart/
