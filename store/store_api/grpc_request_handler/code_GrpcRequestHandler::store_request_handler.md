#1.GrpcRequestHandler::store_request_handler

```
GrpcRequestHandler::store_request_handler
--let QueryRequest {
            action_type,
            param,
            stmt_ctx,
        } = request;
--let action_type = ActionType::from_i32(*action_type);
--let stmt_ctx = StmtCtx::try_from(stmt_ctx)?;
--let ret = match action_type {
            Some(ActionType::GetVertex) => {
                let param = BatchVertexParam::try_from(param)?;
                crate::get_vertex(param, Arc::new(stmt_ctx)).await
            }
            Some(ActionType::GetEdge) => {
                let param = BatchEdgeParam::try_from(param)?;
                crate::get_edge(param, Arc::new(stmt_ctx)).await
            }
            _ => Err(ErrorCode::OtherError("Invalid action type".to_string())),
        };

--let response = match ret {
            Ok(data) => proto::store_api::ReplyMsg {
                status: ReplyStatus::KOk as i32,
                msg: String::default(),
                ret_data: data.try_into().ok(),
            },
            Err(err) => proto::store_api::ReplyMsg {
                status: ReplyStatus::KErr as i32,
                msg: err.to_string(),
                ret_data: None,
            },
        };

--Ok(tonic::Response::new(response))
```