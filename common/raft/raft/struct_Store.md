#1.struct Store

```rust
#[async_trait]
pub trait Store {
    async fn apply(&mut self, message: &[u8]) -> Result<Vec<u8>>;
    async fn query(&self, query: &[u8]) -> Result<Vec<u8>>;
    async fn snapshot(&self) -> Result<Vec<u8>>;
    async fn restore(&mut self, snapshot: &[u8]) -> Result<()>;
    async fn conf_change(&mut self, vote_node: u64, host_id: u64) -> Result<()>;
}

```