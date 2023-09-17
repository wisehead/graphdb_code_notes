#1.GrpcClient::handle_store_request

```
GrpcClient::handle_store_request
--if host_name == MetaHelper::get().get_node_address() {
            let response = GrpcRequestHandler::store_request_handler(&request).await;
            return Self::build_store_grpc_result(&host_name, response).await;
        }

--let response = {
            let tonic_request = GrpcCommon::build_grpc_request(
                request.clone(),
                GrpcCommon::instance().get_computing_grpc_timeout(),
                None,
            );
            let mut client = Self::build_store_grpc_client(&host_name).await?;
            client.handle_remote_query_request(tonic_request).await
        };

--if response.is_err() {
            GrpcChannel::instance().delete_channel(&host_name).await;
        }

--Self::build_store_grpc_result(&host_name, response).await
```