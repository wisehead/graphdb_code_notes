#1.GrpcClient::handle_ddl_request

```
GrpcClient::handle_ddl_request
--if host_name == MetaClient::get().get_node_address() {
----let response = GrpcRequestHandler::ddl_handler(&request).await;
----return GrpcCommon::build_ddl_grpc_result(&host_name, response).await;
```