#1.IdPool::next_id

```
IdPool::next_id
--let mut pool = self.pool.lock().await;
--if pool.start >= pool.end {
            let (start, end) = self.source.apply_next_batch().await?;
            pool.start = start;
            pool.end = end;
--} else {
            pool.start += 1.into();
        }
--Ok(pool.start.clone())
```