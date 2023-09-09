#1.JobManager::get_schedulable_jobs

```
JobManager::get_schedulable_jobs
--let job_id_map = self.job_id_map.read();
--for iter in self.queues.iter() {
----let mut queue = iter.write();
----if id.is_none() {
------continue;
            }
----let job_id = id.unwrap();
----if let Some(data) = job_id_map.get(&job_id) {
------jobs.push(data.clone());
----} else {
------task_warn!("Fail to find job data and remove it from running list");
------queue.remove_running_job(job_id);
----}//end else
--}//end for
```