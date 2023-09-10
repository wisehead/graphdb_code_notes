#1.JobDistribution::dispatch_job

```
JobDistribution::dispatch_job
--let host_list = job_data.get_partition_leaders();
--let raw_spec = RawJobSpec::from(job_data.job_spec.as_ref().to_owned());
--let msg = JobMsg {
            action: action as i32,
            job_spec: serde_json::to_vec(&raw_spec)?,
        };
--let mut join_set = JoinSet::new();
--let mut join_set = JoinSet::new();
--for host in host_list.iter() {
----join_set.spawn_on(
------Self::dispatch_job_to_host(msg.clone(), host.clone(), job_info.clone()),
------BackgroundExecutor::instance().handle(),
            );
--}
--let count = util::build_result_from_joinset(&mut join_set).await?;

```