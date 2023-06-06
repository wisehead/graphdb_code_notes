#1.enum Query

```rust
#[derive(PartialEq, Eq, Debug)]
pub enum Query {
    RegularQuery(RegularQuery),
    StandAloneCall(StandAloneCall),
    Explain(ExplainPlan),
    AlterConfig(AlterConfig),
    DataDefinition(DataDefinition),
    Transaction(Transaction),
    BackendJob(BackendJob),
    DCLDefinition(DCLDefinition),
}

```