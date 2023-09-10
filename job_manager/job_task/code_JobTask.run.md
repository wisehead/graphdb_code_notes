#1.JobTask::run

```
JobTask::run
--if JobTaskCancellation::instance().get_token(job_id).is_some() {
    // Job is already running
----return;
--let job = self.job.clone();
--BackgroundExecutor::instance().spawn(async move {
----let cancel = JobTaskCancellation::instance().create_token(job_id);
----let r = tokio::select!(
                _ = cancel.cancelled() => Ok(()),
                result = job.run()  => result,
            );
----JobTaskCancellation::instance().delete_token(job_id);
----if let Err(e) = r {
                if let Some(handler) = error_handler {
                    // local job
                    handler(TaskId::Int(job_id), e);
                } else if job.is_distribute() {
                    BackgroundExecutor::instance()
                        .spawn(JobDistribution::report_job_status(job_id, JobStatus::Exit));
                }
----} else {
                task_debug!("JobTask::run: job {} run success", job_id);
------if job.is_distribute() {
                    if let Err(e) =
                        JobDistribution::report_job_status(job_id, JobStatus::Done).await
                    {
                        task_error!(
                            "Fail when report job status to ddl leader with error: {:?}",
                            e
                        );
                    }
------} else {
                    task_debug!("update standalone job {} status as JobStatus::Done", job_id);
                    let _ = JobManager::instance()
                        .update_job_status(
                            job_id,
                            MetaClient::get().get_node_address().to_string(),
                            JobStatus::Done,
                        )
                        .await;
------}
----}// end else
--});//BackgroundExecutor::instance().spawn
```