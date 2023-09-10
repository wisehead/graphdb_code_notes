#1.JobDistribution::report_job_status

```
JobDistribution::report_job_status
--let node = meta.get_ddl_leader()?;
--let status_msg = JobStatusMsg {
            job_id: job_id as i32,
            job_status: job_status as i32,
            host: meta.get_node_address().to_string(),
        };
--loop
----let mut client = GrpcCommon::build_ddl_grpc_client(&node.address).await?;
----let tonic_request = GrpcCommon::build_grpc_request(
                status_msg.clone(),
                GrpcCommon::instance().get_computing_grpc_timeout(),
                None,
            );
            // fixme @youbing : if it is local, call function directly
----let response = client.update_job_status(tonic_request).await;
```

#2.GrpcServer::update_job_status

```
GrpcServer::update_job_status
--let msg = request.get_ref();
--let job_manager = JobManager::instance();
--let job_status: JobStatus = msg.job_status.into();
--if !matches!(job_status, JobStatus::New) {
----if matches!(job_status, JobStatus::Exit) {
                        // notify each work to kill the running job task
                        task_info!("notify each worker to kill job task {}", msg.job_id);
                        job_manager.kill_job(msg.job_id as JobId);
----}
----job_manager.update_job_status(msg.job_id as JobId, msg.host.clone(), job_status)
                        .await?;
--}
--Ok(tonic::Response::new(DdlReplyMsg {
                    msg: Some(proto::compute::ReplyMsg {
                        status: (reply_msg::Status::KOk as i32),
                        msg: "".to_string(),
                    }),
                    schema: Some(DataSetMsg::default()),
                    result: vec![],
                }))
```