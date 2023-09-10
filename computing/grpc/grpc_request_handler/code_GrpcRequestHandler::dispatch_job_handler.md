#1.GrpcRequestHandler::dispatch_job_handler

```
GrpcRequestHandler::dispatch_job_handler
--let action = request.action;
--let raw_spec = util::deserialize_msg::<RawJobSpec>(&request.job_spec);
--if let Ok(spec) = raw_spec {
----let job_manager = JobManager::instance();
----match action {
------s if s == JobAction::Check as i32 => {
--------job_manager.check_job(spec.job_id) 
------s if s == JobAction::Run as i32 || s == JobAction::Post as i32
--------let ts = MetaClient::get().get_transaction_ts(false).await?;
--------let job_id = spec.job_id;
--------let job_spec = JobSpec::build(spec, ts);
--------let job_task = JobTask {
----------job_id,
----------job: job_spec.job_info.clone(),
--------};
--------if s == JobAction::Run as i32 {
----------job_task.run(None);
--------} else {
----------job_task.post().await;
--------}
------s if s == JobAction::Kill as i32 => {
                    task_info!("dispatch_job_handler: JobAction::Kill for {:#?}.", spec);
                    if let Some(cancel_token) =
                        JobTaskCancellation::instance().get_token(spec.job_id)
                    {
                        cancel_token.cancel();
                        task_info!("dispatch_job_handler: Job cancelled.");
                    }
------}
------_ => {
                    task_error!("Invalid action in request.");
                    err_msg += "Invalid action in request";
------}
```