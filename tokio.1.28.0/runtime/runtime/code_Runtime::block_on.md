#1.Runtime::block_on

```
Runtime::block_on
--match &self.scheduler {
            Scheduler::CurrentThread(exec) => exec.block_on(&self.handle.inner, future),
            #[cfg(all(feature = "rt-multi-thread", not(tokio_wasi)))]
            Scheduler::MultiThread(exec) => exec.block_on(&self.handle.inner, future),
        }
```

#2.caller

```
- NetworkTaskExecutor::block_on

```