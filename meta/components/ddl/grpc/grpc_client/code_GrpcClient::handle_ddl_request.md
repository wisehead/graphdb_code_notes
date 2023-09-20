#1.GrpcClient::handle_ddl_request

```
GrpcClient::handle_ddl_request
--if host_name == get_node_address() {
----debug_assert!(is_meta_leader());
----let response = GrpcRequestHandler::ddl_handler(&request, true).await;
----return Self::build_ddl_grpc_result(host_name, response).await;
```