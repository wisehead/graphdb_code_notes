#1.JobManager::cancel_job

```
JobManager::cancel_job
--if let Some(job_data) = self.get_job_data(job_id) 
----let mut queue = self.queues[job_group as usize].write();
----if !queue.remove_pend_job(job_id) {
                Err(ErrorCode::CancelRunningJobError(format!(
                    "job {} is running, cannot be canceled",
                    job_id
                )))
----} else {
                // remove this job from system
------let mut job_id_map = self.job_id_map.write();
------job_id_map.remove(&job_id);

                let partition_id = job_data.get_partition_id();
                let graph_id = job_data.get_graph_id();

------BackgroundExecutor::instance().spawn(async move {
                    let _ = MetaClient::get()
                        .delete_job(graph_id, job_id, partition_id)
                        .await;
                });
                Ok(())
----}
```

#2.caller

```
- CancelJobProcessor
```