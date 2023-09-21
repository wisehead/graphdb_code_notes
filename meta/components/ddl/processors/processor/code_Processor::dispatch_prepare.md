#1.Processor::dispatch_prepare

```
Processor::dispatch_prepare
--let local_result = GrpcClient::handle_ddl_request(request.clone(), local_host_name).await;
--let local_result = local_result.unwrap();

  // Handle non-DDL leader hosts
--let (mut success, failure) = GrpcClient::handle_ddl_request_multiple_host(
            host_set
                .iter()
                .map(|x| (x.clone(), request.clone()))
                .collect(),
        )
        .await;
--success.insert(local_host_name.to_string(), local_result);
--if !retain_empty_result {
            success.retain(|_, data_set| !data_set.rows.is_empty());
        }

--if failure.is_empty() {
            return Ok(success);
        }

--host_set.insert(local_host_name.to_string());
  // rollback
--let rollback_request = DdlActionRequest {
            step: DdlStep::KStepRollback as i32,
            ..request.clone()
        };

--if let Err(e) = self.dispatch_post(host_set, rollback_request).await {
            ddl_error!(
                "dispatch_prepare: Fail when dispatch_post to rollback, error: {:?}",
                e
            );
        }
```