#1.start_schedule

```
start_schedule
--job_manager.schedule().await;
```

#2.JobManager::schedule

```
JobManager::schedule
--let notify = self.notify.clone();
--loop {
----let mut jobs: Vec<Arc<JobData>> = vec![];
----while self.get_schedulable_jobs(&mut jobs) {
------count += jobs.len();
------for job in jobs.iter() {
--------BackgroundExecutor::instance().spawn(Self::run_job(job.clone()));
----notify.notified().await;
--}//loop end
```