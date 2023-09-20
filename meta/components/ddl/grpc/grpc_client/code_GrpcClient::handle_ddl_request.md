#1.GrpcClient::handle_ddl_request

```
GrpcClient::handle_ddl_request
--if host_name == get_node_address() {
----debug_assert!(is_meta_leader());
----let response = GrpcRequestHandler::ddl_handler(&request, true).await;
----return Self::build_ddl_grpc_result(host_name, response).await;
--let mut count: i32 = GrpcCommon::instance().get_retry_count() + 1;
--loop {
            let response = {
                let tonic_request = GrpcCommon::build_grpc_request(
                    request.clone(),
                    GrpcCommon::instance().get_computing_grpc_timeout(),
                    None,
                );
                let mut client = GrpcCommon::build_ddl_grpc_client(host_name).await?;
                client.handle_ddl_request(tonic_request).await
            };
            count -= 1;
            if response.is_err() && count > 0 {
                GrpcChannel::instance().delete_channel(host_name).await;
                continue;
            }

            return Self::build_ddl_grpc_result(host_name, response).await;
        }
```