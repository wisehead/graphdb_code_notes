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
```

#2.caller

```
- with_budget
```