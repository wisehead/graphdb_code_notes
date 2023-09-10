#1.struct JobTaskCancellation

```
pub struct JobTaskCancellation {
    cancel_token: RwLock<HashMap<JobId, Arc<CancellationToken>>>,
}

```