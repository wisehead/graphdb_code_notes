#1.JobManager::instance

```
JobManager::instance
--let manager = Arc::new(Self::new());
--BackgroundExecutor::instance().spawn(start_schedule(manager.clone()));
```

#2.JobManager::new

```
JobManager::new
--let mut queues = vec![];
        // all defined job groups
--let group = JobGroup::get_all_group();
--for g in group {
----let queue = JobQueue::new(g, Config::get_max_jobs(g));
----queues.push(RwLock::new(queue));
--Self {
            queues,
            job_id_map: RwLock::new(HashMap::new()),
            notify: Arc::new(Notify::new()),
        }

```