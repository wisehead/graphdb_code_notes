#1.GrpcRequestHandler::ddl_handler

```
GrpcRequestHandler::ddl_handler
--let step = request.step;
--match &mut DDLOperator::from_grpc_msg(request) {
----Ok(executor) => match executor.process_with_step(step).await {
                // Success
------Ok(r) => reply_msg.schema = Some(r),
--reply_msg.msg = if error_msg.is_empty() {
----Some(ReplyMsg {
                status: (reply_msg::Status::KOk as i32),
                msg: "".to_string(),
            })
--Ok(tonic::Response::new(reply_msg))
```