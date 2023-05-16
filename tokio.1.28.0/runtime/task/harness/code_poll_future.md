#1.poll_future

```
poll_future
--panic::catch_unwind(panic::AssertUnwindSafe(|| {})
----//lambda
----guard.core.poll(cx);
--// Prepare output for being placed in the core stage.
    let output = match output {
        Ok(Poll::Pending) => return Poll::Pending,
```