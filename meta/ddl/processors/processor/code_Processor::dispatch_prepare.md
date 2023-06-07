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
```