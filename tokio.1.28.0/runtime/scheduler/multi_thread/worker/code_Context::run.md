#1.Context::run

```
Context::run
--while !core.is_shutdown {
----core.tick();
----core = self.maintenance(core);
----if let Some(task) = core.next_task(&self.worker) {
                core = self.run_task(task, core)?;
                continue;
            }

```