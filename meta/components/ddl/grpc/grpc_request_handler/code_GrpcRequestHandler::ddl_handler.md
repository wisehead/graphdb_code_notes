#1.GrpcRequestHandler::ddl_handler

```
GrpcRequestHandler::ddl_handler
--match &mut DDLOperator::from_grpc_msg(request) {
----Ok(executor) => match executor.process_with_step(step, is_meta_leader).await {
      // Success
------Ok(r) => reply_msg.result = r.into_rmp_msg(),
      // operation failure
------Err(err) => error_msg += format!("{:?}", err).as_str(),
--},
----Err(err) => {
                // internal error (invalid data)
                error_msg += format!("{:?}", err).as_str();
            }
--}
--reply_msg.msg = if error_msg.is_empty() {
            Some(ReplyMsg {
                status: (reply_msg::Status::KOk as i32),
                msg: "".to_string(),
            })
        } else {
            Some(ReplyMsg {
                status: (reply_msg::Status::KErr as i32),
                msg: error_msg,
            })
        };

--Ok(tonic::Response::new(reply_msg))
```