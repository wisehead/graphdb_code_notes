#1.Processor::dispatch_post
```
Processor::dispatch_post
--let (_, mut failure) = GrpcClient::handle_ddl_request_multiple_host(
            host_set
                .iter()
                .map(|x| (x.clone(), request.clone()))
                .collect::<HashMap<String, DdlActionRequest>>(),
        )
        .await;
--if flag {
            if let Err(err) = GrpcClient::handle_ddl_request(request.clone(), local_host).await {
                failure.insert(local_host.to_string(), err);
            }
        }
--if failure.is_empty() {
            return Ok(());
        }
--let failure_hosts: Vec<String> = failure.into_keys().collect();
--let code = match request.step {
            s if s == DdlStep::KStepCleanup as i32 => {
                let message = format!("fail to cleanup on hosts: {:?}", failure_hosts);
                ErrorCode::DDLCleanupError(message)
            }
            s if s == DdlStep::KStepRollback as i32 => {
                let message = format!("fail to rollback on hosts: {:?}", failure_hosts);
                ErrorCode::DDLRollbackError(message)
            }
            _ => {
                let message = format!("hit exception on hosts: {:?}", failure_hosts);
                ErrorCode::DDLExceptionError(message)
            }
        };        
```