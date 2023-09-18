#1.GrpcClient::build_store_grpc_client

```
GrpcClient::build_store_grpc_client
--let channel = GrpcChannel::instance().get_channel(host).await?;
--let client = store_api_service_client::StoreApiServiceClient::new(channel);
```