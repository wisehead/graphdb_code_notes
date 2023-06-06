#1.GrpcCommon::build_ddl_grpc_client

```
GrpcCommon::build_ddl_grpc_client
--let channel = GrpcChannel::instance().get_channel(host).await?;
--let client = ddl_service_client::DdlServiceClient::new(channel);
```