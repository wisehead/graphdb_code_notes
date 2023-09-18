#1.enum MetaStore

```rust
pub enum MetaStore {
    Etcd(EtcdProcessor),
    Rocksdb(RocksDBProcessor),
}

```