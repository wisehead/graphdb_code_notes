#.QueryServiceExecutor::instance

```
QueryServiceExecutor::instance
--EXECUTOR
            .get_or_init(|| {
                let thread = std::thread::spawn(Self::init);
                if let Ok(value) = thread.join() {
                    value
                } else {
                    panic!("Fail to init QueryServiceExecutor")
                }
            })
            .inner
            .clone()

```

#2.caller

```
- main
```