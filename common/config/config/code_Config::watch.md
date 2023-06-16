#1.Config::watch

```
Config::watch
--let file_contents = std::fs::read(&config_path); 
--let file_contents = file_contents.unwrap();
--let new_md5 = md5::compute(&file_contents);
--if new_md5 == old_md5 {
----continue;
--old_md5 = new_md5;
--let config = Config::from_config_file(Path::new(&config_path));
--let log_guard = arcgraph_log::logger::get_log_guard(&config.log);
--if log_guard.audit_reload_handle.is_some() {
----let ret = log_guard
                    .audit_reload_handle
                    .as_ref()
                    .unwrap()
                    .modify(|filter| *filter = EnvFilter::new(&config.log.audit_env));
--if log_guard.reload_handle.is_some() {
----let ret = log_guard
                    .reload_handle
                    .as_ref()
                    .unwrap()
                    .modify(|filter| *filter = EnvFilter::new(&config.log.env));
```