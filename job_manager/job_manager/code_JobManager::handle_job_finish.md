#1.JobManager::handle_job_finish

```
JobManager::handle_job_finish
--let job_data = {
            let job_id_map = self.job_id_map.read();
            job_id_map.get(&job_id).cloned()
        };
--if let Some(job_data) = job_data {
----let job_group = job_data.get_job_group();

----match job_status {
------JobStatus::Done => {
                    // remove job information
                    let mut queue = self.queues[job_group as usize].write();
                    queue.remove_running_job(job_id);
                    let mut job_id_map = self.job_id_map.write();
                    job_id_map.remove(&job_id);
                    task_trace!("delete job {} from job map", job_id);
------}
------JobStatus::ExitAll => {
                    task_trace!("move job {} to new job list", job_id);
                    let mut queue = self.queues[job_group as usize].write();
                    queue.add_job(job_id, true);
------}
------_ => {}
----}
--}
```