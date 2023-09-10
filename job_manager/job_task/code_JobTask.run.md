#1.JobTask::run

```
JobTask::run
--if JobTaskCancellation::instance().get_token(job_id).is_some() {
    // Job is already running
----return;
```