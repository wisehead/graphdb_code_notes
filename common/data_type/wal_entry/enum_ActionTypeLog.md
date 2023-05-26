#1.enum ActionTypeLog

```
#[repr(i8)]
#[derive(Clone, Serialize, Deserialize, Debug)]
pub enum ActionTypeLog {
    StartTxn = 0,
    CommitTxn = 1,
    RollbackTxn = 2,
    InsertVertex = 3,
    UpdateVertex = 4,
    DeleteVertex = 5,
    InsertEdge = 6,
    UpdateEdge = 7,
    DeleteEdge = 8,
    Checkpoint = 9,
    SyncLSN = 10,
}

```