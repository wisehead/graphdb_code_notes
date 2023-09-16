#1.trait KvClientInterface

```rust
pub trait KvClientInterface {
    async fn key_exists(&self, key: Key) -> Result<bool>;

    async fn get(&self, key: Key) -> Result<Option<Value>>;

    async fn batch_get(&self, keys: Vec<Key>) -> Result<HashMap<Key, Value>>;

    async fn scan(&self, range: Range, limit: u32) -> Result<Vec<KvPair>>;

    async fn scan_key(&self, range: Range, limit: u32) -> Result<Vec<Key>>;

    async fn batch_put(&self, pairs: Vec<KvPair>) -> Result<()>;

    async fn batch_delete(&self, keys: Vec<Key>) -> Result<()>;

    async fn delete_range(&self, range: Range) -> Result<()>;

    async fn txn_get(&self, key: &str, prefix: bool) -> Result<Vec<KvPair>>;

    async fn txn_put(&self, kvs: &HashMap<String, String>) -> Result<()>;

    async fn txn_delete(&self, keys: &HashMap<String, bool>) -> Result<()>;

    async fn txn_put_comparison(
        &self,
        key: String,
        value: String,
        comparison: Comparison,
    ) -> Result<()>;
}
```