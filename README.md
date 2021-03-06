# tp_go_grpc

grpc的全功能服务端和对应测试客户端模板.

该模板提供如下特性:

1. 本地负载均衡
2. 基于dns的负载均衡
3. 基于xds的负载均衡
4. meta数据传输
5. 拦截器
6. 健康检查
7. 反射接口
8. 可配置的数据压缩
9. 可配置的性能优化项
10. channelz特性
11. grpc-gateway以及其对应的swagger测试界面

需要注意

1. 服务端的xds支持目前并不完善,使用服务端xds可以实现服务注册,但同时会失去反射接口,并且健康监测将不在同一个端口而是在服务端口号加1上实现.
2. v2.0.0及以上版本都不再支持go 1.18以下的版本.如果使用低版本的go语言,请使用v0版本
3. v2版本已经和tp_go_grpcsimple模板合并.直接使用该模板不会带拦截器模板(只提供注释掉的接入演示),如果需要使用拦截器,可以通过`ppm project add cp_go_grpc@2.0.0//servinterceptor | cp_go_grpc@2.0.0//sdkinterceptor`来添加.
4. 使用如下命令编译proto文件

    ```bash
        protoc -I pbschema \
        --go_out . \
        --go-grpc_out . \
        --grpc-gateway_out . \
        --grpc-gateway_opt logtostderr=true \
        --openapiv2_out ./{{ serv_name }}_serv \
        --openapiv2_opt logtostderr=true \
        {{ serv_name }}.proto
    ```
