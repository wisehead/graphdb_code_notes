#1.GrpcChannel::get_channel

```
GrpcChannel::get_channel
--let timestamp = SystemTime::now()
            .duration_since(UNIX_EPOCH)
            .unwrap()
            .as_secs();
--let lock = self.channels.read();
--if let Some(entry) = lock.get(host) && timestamp < entry.timestamp {
----return Result::Ok(entry.channel.clone());
--let channel = self.build_channel(host).await?;
--self.insert_channel(
            host,
            &channel,
            timestamp + self.connection_cache_ttl.load(Ordering::SeqCst),
        );
```