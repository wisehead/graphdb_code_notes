#1.MultiThread::block_on

```
MultiThread::block_on
--let mut enter = crate::runtime::context::enter_runtime(handle, true);
--enter
            .blocking
            .block_on(future)
            .expect("failed to park thread")
----BlockingRegionGuard::block_on
```

#2.caller

```
Runtime::block_on
```