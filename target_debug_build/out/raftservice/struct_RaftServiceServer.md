#1.struct RaftServiceServer

```rust
    #[derive(Debug)]
    pub struct RaftServiceServer<T: RaftService> {
        inner: _Inner<T>,
        accept_compression_encodings: (),
        send_compression_encodings: (),
    }

```