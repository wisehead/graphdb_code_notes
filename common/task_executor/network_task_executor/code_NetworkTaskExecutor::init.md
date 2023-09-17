#1.NetworkTaskExecutor::init

```
NetworkTaskExecutor::init
--let total_num = num_cpus::get();

--let thread_num = if total_num > 0 {
            if pool_size == 0 || pool_size > total_num {
                total_num
            } else {
                pool_size
            }
--} else {
            std::cmp::max(1, pool_size)
        };

--let thread_name = format!("{} IO-worker", name);
--let runtime = if thread_num == 1 {
            tokio::runtime::Builder::new_current_thread()
                .enable_all()
                .thread_name(thread_name)
                .build()?
--} else {
            tokio::runtime::Builder::new_multi_thread()
                .enable_all()
                .thread_name(thread_name)
                .worker_threads(thread_num)
                .build()?
        };

--std::io::Result::Ok(NetworkTaskExecutor { inner: runtime })

```