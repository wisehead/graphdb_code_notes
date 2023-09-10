#1.JobDistribution::dispatch_job_to_host

```
JobDistribution::dispatch_job_to_host
--let mut count = GrpcCommon::instance().get_retry_count() + 1;
--loop {
----let mut client = GrpcCommon::build_compute_grpc_client(&hostname).await?;
----let tonic_request = GrpcCommon::build_grpc_request(
                job_msg.clone(),
                GrpcCommon::instance().get_computing_grpc_timeout(),
                None,
            );
----let response = client.dispatch_job(tonic_request).await;
```

#2.GrpcServer::dispatch_job

```
GrpcServer::dispatch_job
--GrpcRequestHandler::dispatch_job_handler(request.get_ref()).await
```