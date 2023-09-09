#1.JobQueue::get_next_pend_job

```
JobQueue::get_next_pend_job
--let run = self.running_jobs.len();
--if self.pending_jobs.is_empty() || run >= self.max_run_jobs {
            return None;
--}

--loop {
----let job_id = self.pending_jobs.pop_front()?;

----if self.cancelled_jobs.contains(&job_id) {
                // return next valid ID if job has already
                // been marked as cancelled
                self.cancelled_jobs.remove(&job_id);
----} else {
                if schedule {
                    self.running_jobs.insert(job_id);
                }
                return Some(job_id);
----}
--}

```