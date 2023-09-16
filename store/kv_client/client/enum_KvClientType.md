#1.enum KvClientType

```rust
pub enum KvClientType {
    Etcd {
        endpoints: Vec<String>,
        username: Option<String>,
        password: Option<String>,
    },
    Rocksdb {
        db_path: String,
    },
    RocksdbTxn {
        db_path: String,
    },
    TiKV {
        pd_address: Vec<String>,
    },
}
```