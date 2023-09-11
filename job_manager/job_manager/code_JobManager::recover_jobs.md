#1.JobManager::recover_jobs

```
JobManager::recover_jobs
--let mut job_map: HashMap<JobGroup, Vec<JobId>> = HashMap::new();
--let mut id_map = self.job_id_map.write();
--for iter in raw_specs {
            let spec = JobSpec::build(iter, ts.clone());
            let job_data = Arc::new(JobData::new(Arc::new(spec)));

            let job_id = job_data.get_job_id();
            let job_group = job_data.get_job_group();

            let entry = job_map.entry(job_group).or_default();
            entry.push(job_id);

            id_map.insert(job_id, job_data);
--}

--for (group, mut job_ids) in job_map {
            let mut queue = self.queues[group as usize].write();
            job_ids.sort();
            queue.recover_jobs(job_ids);
--}
--self.notify();
```