# Environment

```bash
# In the Dcoker Container
$ go version
go version go1.18.2 linux/amd64
$ protoc --version
libprotoc 3.12.4
```

Unity 2021.3.3f1

# genererate gRPC code for golang server
In the `realtime-grpc`dir ( workspace root dir) , run the following command:
```
$ protoc --go_out=. --go_opt=paths=source_relative  --go-grpc_out=. --go-grpc_opt=paths=source_relative    proto/world/user.proto proto/world/room.proto 
```

# generate gRPC code for csharp client


1. download `grpc-protoc_linux_x64-1.47.0-dev.tar.gz` in gRPC protoc Plugins from [Artifacts for gRPC Build f15a2c1c-582b-4c51-acf2-ab6d711d2c59](https://packages.grpc.io/archive/2022/04/67538122780f8a081c774b66884289335c290cbe-f15a2c1c-582b-4c51-acf2-ab6d711d2c59/index.xml)
    - may be curl is ok
1. copy to docker container
    ```
    cp -R path_to_downloads/Grpc.Tools . 
    ```
1. In the `realtime-grpc`dir ( workspace root dir) , run the following command:
    ```
    protoc --proto_path=. --csharp_out=proto/world --grpc_out=proto/world proto/world/user.proto proto/world/room.proto --plugin=protoc-gen-grpc=Grpc.Tools/tools/linux_x64/grpc_csharp_plugin
    ```
    Room.cs,RoomGrpc.cs,User.cs are generated

# Set up in Unity Editor

1. download  `grpc_unity_package.2.47.0-dev202204190851.zip` in C# from [Artifacts for gRPC Build f15a2c1c-582b-4c51-acf2-ab6d711d2c59](https://packages.grpc.io/archive/2022/04/67538122780f8a081c774b66884289335c290cbe-f15a2c1c-582b-4c51-acf2-ab6d711d2c59/index.xml)
1. unzip grpc_unity_package.2.47.0-dev202204190851.zip and put on Assets dir in Unity Project
1. In Unity Editor , File -> Build Settings -> Player Settings -> Other Settings -> set `.Net Framework` on Api Compatibility Level
1. Implement Client Code.
    ref [client | gRPC](https://grpc.io/docs/languages/csharp/basics/#client)

# reference
- [gRPC で実現する Unity と Go 使ってカメラの位置/回転を同期させる方法 - Qiita](https://qiita.com/nikaera/items/e8c7ef217dce17652872)
- [Protocol bufferとgolangの勉強とUnity+Go(docker)のgRPCリアルタイムサーバーの実装](https://zenn.dev/toutou/scraps/8f8be25de10d1b)