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