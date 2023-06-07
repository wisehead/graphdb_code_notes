#1.GrpcClient::handle_ddl_request_multiple_host

```
GrpcClient::handle_ddl_request_multiple_host
--let mut tasks = HashMap::new();
--for (key, value) in request {
----tasks.insert(
                key.clone(),
                QueryEngineExecutor::instance().spawn(Self::handle_ddl_request(value, key)),
            );
------GrpcClient::handle_ddl_request
--------ddl_service_client::DdlServiceClient:: handle_ddl_request
----------GrpcServer::handle_ddl_request
------------ddl::GrpcRequestHandler::ddl_handler(request.get_ref()).await
--------------executor.process_with_step(step).await
--for (key, value) in tasks {
            let (task_result,) = tokio::join!(value);
            match task_result {
                Ok(result) => match result {
                    Ok(t) => _ = success.insert(key, t),
                    Err(code) => _ = failure.insert(key, code),
                },
                Err(err) => _ = failure.insert(key, ErrorCode::from(err)),
            }
        }
```