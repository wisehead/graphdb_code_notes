#1.JobQueue::new

```
JobQueue::new
--Self {
            group,
            priority: 0,
            retry_times: 0,
            max_run_jobs,
            pending_jobs: VecDeque::new(),
            running_jobs: HashSet::new(),
            cancelled_jobs: HashSet::new(),
        }
```