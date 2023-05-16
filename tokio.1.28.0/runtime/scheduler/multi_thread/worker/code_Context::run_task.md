#1.Context::run_task

```
Context::run_task
--coop::budget(|| {
----//lambda
----task.run();
----loop
------let mut core = match self.core.borrow_mut().take() {
                    Some(core) => core,
                    None => return Err(()),
                };
------let task = match core.lifo_slot.take() {
                    Some(task) => task,
                    None => return Ok(core),
                };
------if coop::has_budget_remaining() {
--------core.metrics.incr_poll_count();
--------*self.core.borrow_mut() = Some(core);
--------let task = self.worker.handle.shared.owned.assert_owner(task);
--------task.run();
```

#2.caller

```
- Context::run
```