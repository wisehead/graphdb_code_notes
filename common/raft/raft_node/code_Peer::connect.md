#1.Peer::connect

```
Peer::connet
--if let Some(c) = self.client.read().await.as_ref() {
----return Ok(c.clone());
--let mut client = self.client.write().await;
--if let Some(c) = client.as_ref() {
----return Ok(c.clone());
--let endpoint = self._endpoint()?;
--let c = Self::_connect(&endpoint, self.crw_timeout).await?;
--client.replace(c.clone());
```

#2.Peer::_endpoint

```rust
 fn _endpoint(&self) -> Result<Endpoint> {
        let endpoint = Channel::from_shared(format!("http://{}", self.addr))
            .map(|endpoint| {
                endpoint
                    .concurrency_limit(self.concurrency_limit)
                    .timeout(self.crw_timeout)
            })
            .map_err(|e| Error::Other(Box::new(e)))?;
        Ok(endpoint)
    }
```

#3.Peer::_connect

```rust
async fn _connect(endpoint: &Endpoint, crw_timeout: Duration) -> Result<RaftGrpcClient> {
        let channel = tokio::time::timeout(crw_timeout, endpoint.connect())
            .await
            .map_err(|e| Error::Other(Box::new(e)))?
            .map_err(|e| Error::Other(Box::new(e)))?;
        let client = RaftServiceClient::new(channel);
        Ok(client)
    }
```