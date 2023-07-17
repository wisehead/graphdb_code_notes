#1.Processor::route_result

```
Processor::route_result
--match ctx.next_op_id {
----Some(id) => ctx.pipeline.process_by_operator_id(id, data).await,
----None => {
------let res = GrpcClient::send_result(
                    ctx.op_info.into_grpc_id(),
                    vec![*data],
                    ctx.op_info.master_name.as_str(),
                    true,
                )
------match ctx.pipeline {
--------PipelineRef::MainPipeline(_) => {}
--------PipelineRef::WorkerPipeline(_) => {
----------if !ctx.is_running.load(Ordering::SeqCst) {
------------let p = PipelineFamilyManager::instance()
                                .get_pipeline_family(&ctx.op_info.main_pipeline_id)
                                .unwrap();
------------p.wait().await;
                        }
                    }
                }                
----}
```