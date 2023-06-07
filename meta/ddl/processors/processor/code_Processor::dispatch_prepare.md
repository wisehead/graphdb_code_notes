#1.Processor::dispatch_prepare
```
Processor::dispatch_prepare
--let local_host_name = MetaClient::get().get_node_address();
--let mut host_set = self.get_all_nodes();
--host_set.remove(&local_host_name);
--GrpcClient::handle_ddl_request(request.clone(), local_host_name.clone()).await?;
--get_node_info(&local_host_name, local_result)?;
--// Handle non-DDL leader hosts
--let (success, mut failure) = GrpcClient::handle_ddl_request_multiple_host(
            host_set
                .iter()
                .map(|x| (x.clone(), request.clone()))
                .collect(),
        )
        .await;
--let mut host_set = HashSet::from([local_host_name]);
--for (key, value) in success {
            match get_node_info(&key, value) {
                Ok(address) => {
                    host_set.insert(address);
                }
                Err(err) => {
                    failure.insert(key, err);
                }
            }
        }       
--if failure.is_empty() {
----return Ok(()); 

  //rollback
--let rollback_request = DdlActionRequest {
            step: DdlStep::KStepRollback as i32,
            ..request.clone()
        };
--let _ = self.dispatch_post(host_set, rollback_request).await;        
```