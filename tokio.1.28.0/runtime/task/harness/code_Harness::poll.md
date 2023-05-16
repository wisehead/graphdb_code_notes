#1.Harness::poll

```
Harness::poll
--match self.poll_inner() {
----PollFuture::Notified => {
                // The `poll_inner` call has given us two ref-counts back.
                // We give one of them to a new task and call `yield_now`.
                self.core()
                    .scheduler
                    .yield_now(Notified(self.get_new_task()));

                // The remaining ref-count is now dropped. We kept the extra
                // ref-count until now to ensure that even if the `yield_now`
                // call drops the provided task, the task isn't deallocated
                // before after `yield_now` returns.
                self.drop_reference();
            }

```

#2.caller

```
//raw.rs
poll

```