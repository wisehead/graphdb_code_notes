#1.QueryServiceExecutor::init

```
QueryServiceExecutor::init
--let query_service_thread_number = SystemConfigManager::instance().get_value_into::<usize>(
            SERVER_QUERY_SERVICE_THREAD_NUMBER,
            &config::ConfigType::Config,
        );
--let inner = NetworkTaskExecutor::init(query_service_thread_number, "QueryService")
            .expect("Fail to init QueryServiceExecutor");

--Self {
            inner: Arc::new(inner),
        }
```