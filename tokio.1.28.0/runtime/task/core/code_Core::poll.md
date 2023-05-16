#1.Core::poll

```
Core::poll
--self.stage.stage.with_mut(|ptr| {
                // Safety: The caller ensures mutual exclusion to the field.
                let future = match unsafe { &mut *ptr } {
                    Stage::Running(future) => future,
                    _ => unreachable!("unexpected stage"),
                };

                // Safety: The caller ensures the future is pinned.
                let future = unsafe { Pin::new_unchecked(future) };

                let _guard = TaskIdGuard::enter(self.task_id);
                future.poll(&mut cx)
            })

```

#2.caller

```
- poll_future
```