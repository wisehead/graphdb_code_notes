#1.TaskManager::insert_task

```
TaskManager::insert_task
--let mut tasks = self.tasks.lock();
--let entry = tasks.entry(id.clone()).or_default();
--entry.push_back(task);

--if let Some(callback) = error_handler {
            let mut map = self.error_handler.write();
            map.insert(id, Box::new(callback));
        }

--self.cond_var.notify_all();
```