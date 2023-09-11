#1.TaskManager::handle_tasks

```
TaskManager::handle_tasks
--let mut tasks = manager.tasks.lock();
--loop {
----for (key, value) in tasks.iter_mut() {
------if value.is_empty() {
--------continue;
------}
------let task_vec = value.drain(0..).collect::<Vec<_>>();
------BackgroundExecutor::instance().spawn(Self::join_tasks(task_vec, key.clone()));
----}//end for

----manager.cond_var.wait(&mut tasks);
--}

```