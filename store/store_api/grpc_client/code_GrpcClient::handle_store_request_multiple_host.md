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
```