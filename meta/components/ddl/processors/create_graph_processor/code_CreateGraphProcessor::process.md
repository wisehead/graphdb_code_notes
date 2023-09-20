#1.CreateGraphProcessor::process

```
CreateGraphProcessor::process
--if !is_meta_leader() {
----let request = self.create_request(DdlStep::KStepForward, stmt_ctx)?;
----return self.forward(request).await;
```