#1.DdlGrpcService::handle_ddl_request

```
DdlGrpcService::handle_ddl_request
--let r = BackgroundExecutor::instance()
            .spawn(
                async move { ddl::GrpcRequestHandler::ddl_handler(request.get_ref(), false).await },
            )
            .await;
```