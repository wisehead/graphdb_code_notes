#1.JobManager::run_job

```
JobManager::run_job
--if job_data.reach_retry_limit() {
----let job_group = job_data.get_job_group();
----let manager = JobManager::instance();
----let mut queue = manager.queues[job_group as usize].write();
----queue.remove_running_job(job_id);
            // fail job will never be re-run before job recover
----task_error!("Job {job_id} fails and reaches the retry limit.");
----return;
--}
--// run job
--let status_map = {
----if job_data.is_distribute() {
                // Distribute mode
                job_data.init_status(job_data.get_partition_leaders(), JobStatus::Run);
                let result = JobDistribution::dispatch_job(job_data.clone(), JobAction::Run).await;
                if result.is_err() {
                    let job_group = job_data.get_job_group();
                    let manager = JobManager::instance();
                    let mut queue = manager.queues[job_group as usize].write();
                    queue.add_job(job_id, true);
                    return;
                }
----} else {
      // Standalone mode
------let job_task = JobTask {
                    job_id,
                    job: job_data.job_spec.job_info.clone(),
------};
------job_data.init_status(
                    vec![MetaClient::get().get_node_address().to_string()],
                    JobStatus::Run,
------);
------job_task.run(Some(JobManager::mark_standalone_job_error));
----}

----job_data.job_status.read().clone()
--};//end run job
```