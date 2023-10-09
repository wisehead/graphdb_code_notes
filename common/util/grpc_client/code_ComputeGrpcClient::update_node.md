#1.ComputeGrpcClient::update_node

```
ComputeGrpcClient::update_node
--let grpc_common = GrpcCommon::instance();
--let mut retry = grpc_common.get_retry_count();

--loop {
----retry -= 1;
----let result = Self::update_node_implement(&host, &msg).await;
----return Ok(());
--}
```

#2.update_node_implement
```
update_node_implement
--let mut client = GrpcCommon::build_compute_grpc_client(host).await?;
--let tonic_request = GrpcCommon::build_grpc_request(
            msg.to_owned(),
            Some(GrpcCommon::instance().get_computing_grpc_timeout()),
            None,
        );
--client.update_node(tonic_request).await?;
```