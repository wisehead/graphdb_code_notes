#1.struct LogEntry

```
#[derive(Clone, Serialize, Deserialize, Debug)]
pub struct LogEntry {
    pub lsn: u64,
    pub txn_id: TransactionId,
    pub term: i64,
    pub action_type: ActionTypeLog,
    // "action_log" is "None" for StartTxn/CommitTxn/RollbackTxn/Checkpoint
    pub action_log: Option<GraphObjectLog>,
}

```