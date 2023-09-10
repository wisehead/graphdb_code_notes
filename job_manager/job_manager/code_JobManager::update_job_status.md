#1.JobManager::update_job_status

```
JobManager::update_job_status
--let job_data = {
            let id_map = self.job_id_map.read();
            id_map.get(&job_id).cloned()
        };
--let old_status = data.get_job_status();
--let status_map: HashMap<String, JobStatus> = {
----let mut job_status = data.job_status.write();
                task_debug!("job {} old status map is {:?}", job_id, job_status);
----if let Entry::Occupied(mut entry) = job_status.entry(host.clone()) {
                    task_trace!(
                        "host {} updated status as {:?} for job {}",
                        host,
                        status,
                        job_id
                    );
                    entry.insert(status);
----} else {
                    task_info!(
                        "Invalid host {} reported status {:?} for job {}",
                        host,
                        job_status,
                        job_id
                    );
                    return Ok(());
----}
----job_status.clone()
--};
--let job_status = data.get_job_status();
--if old_status.is_finished() {
                // Job is already gone
----if job_status == JobStatus::ExitAll {
                    task_info!("Put job {} in new job list", job_id);
                    let group = data.get_job_group();
                    let mut queue = self.queues[group as usize].write();
                    queue.add_job(job_id, true);
                    self.notify();
----return Ok(());
--}
--if job_status == JobStatus::Done {
----let result = JobDistribution::dispatch_job(data.clone(), JobAction::Post).await;
----result?;
--if job_status.is_finished() {
----task_debug!("job {} finished with {:?}", job_id, job_status);
----self.handle_job_finish(job_id, &job_status).await;
----data.job_spec.job_info.update(JobStatus::Done).await?;
----self.notify();
--if job_status.is_exited() {
----return MetaClient::get().put_job_status(job_id, status_map).await;
--} else if job_status == JobStatus::Done {
----data.job_spec.job_info.update(JobStatus::Done).await?;
----return MetaClient::get()
                    .delete_job(data.get_graph_id(), job_id, data.get_partition_id())
                    .await;
--}
```