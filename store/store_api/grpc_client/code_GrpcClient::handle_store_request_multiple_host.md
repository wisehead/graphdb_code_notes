#1.GrpcClient::handle_store_request_multiple_host

```
GrpcClient::handle_store_request_multiple_host
--let mut tasks = HashMap::new();
--for (key, value) in request {
----tasks.insert(
                key.clone(),
                QueryServiceExecutor::instance()
                    .spawn(Self::handle_store_request(value, key).in_current_span()),
            );
--}
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