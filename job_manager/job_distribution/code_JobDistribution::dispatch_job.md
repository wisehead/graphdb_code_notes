#1.JobDistribution::dispatch_job

```
JobDistribution::dispatch_job
--let host_list = job_data.get_partition_leaders();
--let raw_spec = RawJobSpec::from(job_data.job_spec.as_ref().to_owned());
--let msg = JobMsg {
            action: action as i32,
            job_spec: serde_json::to_vec(&raw_spec)?,
        };
--
```