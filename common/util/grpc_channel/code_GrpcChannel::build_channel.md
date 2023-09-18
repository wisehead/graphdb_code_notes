## #1.GrpcChannel::build_channel

```
GrpcChannel::build_channel
--let mut retry: i32 = self.connect_retry.load(Ordering::SeqCst);

--let mut end_point = Endpoint::try_from(format!("http://{}", host))?;
--let timeout = self.connect_timeout.load(Ordering::SeqCst);
--if timeout > 0 {
            end_point = end_point.connect_timeout(Duration::from_secs(timeout))
        }

--end_point = end_point.concurrency_limit(self.concurrency_limit.load(Ordering::SeqCst));

--end_point = end_point.keep_alive_while_idle(true);

--loop {
----let ret = end_point.connect().await;
----match ret {
                Ok(c) => {
                    return Result::Ok(c);
                }
                Err(err) => {
                    retry -= 1;
                    if retry < 0 {
                        arcgraph_log::comm_warn!("fail to connect host {}", host);
                        return Result::Err(ErrorCode::from(err));
                    } else {
                        continue;
                    }
                }
            }
        }
```