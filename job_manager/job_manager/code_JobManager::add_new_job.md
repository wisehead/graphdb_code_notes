#1.JobManager::add_new_job

```
JobManager::add_new_job
--let graph_id = job_spec.job_info.get_graph_id();
--job_spec.job_info.update(JobStatus::New).await?;
--let raw_job_spec = RawJobSpec::from(job_spec.as_ref().to_owned());
----let job_id = job_spec.job_id;
----let job = Arc::new(JobData::new(job_spec));
----let group = job.get_job_group();

----let mut map = self.job_id_map.write();
----map.insert(job_id, job);

----let mut queue = self.queues[group as usize].write();
----queue.add_job(job_id, false);

----MetaClient::get()
            .put_job_spec(graph_id, raw_job_spec)
            .await?;
----self.notify();
```