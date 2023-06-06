#1.GrpcRequestHandler::ddl_handler

```
GrpcRequestHandler::ddl_handler
--let step = request.step;
--match &mut DDLOperator::from_grpc_msg(request) {
----Ok(executor) => match executor.process_with_step(step).await {
                // Success
------Ok(r) => reply_msg.schema = Some(r),
```