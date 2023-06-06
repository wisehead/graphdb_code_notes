#1.parse_query

```
parse_query
--#map(rule!{#parse_regular_query}, Query::RegularQuery) |
--#map(rule!{#explain_plan}, Query::Explain) |
--// #map(rule!{#parse_alter_config}, Query::AlterConfig) |
--#map(rule!{#parse_ddl}, Query::DataDefinition) |
--#map(rule!{#parse_transaction}, Query::Transaction) |
--#map(rule!{#parse_backend_job}, Query::BackendJob) |
--#map(rule!{#parse_dcl}, Query::DCLDefinition) |
--#map(rule!{#parse_call}, Query::StandAloneCall)
```