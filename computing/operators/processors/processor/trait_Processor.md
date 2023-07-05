#1.trait Processor

```rust
async fn do_process(&self, data: Box<OpData>, ctx: ProcessContext<'async_trait>) -> Result<()>;

    async fn flush(&self, _ctx: ProcessContext<'async_trait>) -> Result<()> {
        operator_debug!("processor do flush");
        Ok(())
    }

    async fn pre_write(&self, _ctx: Arc<QueryContext>, _src_host: String) -> Result<()> {
        Ok(())
    }

    #[allow(clippy::too_many_arguments)]
    async fn write_to_ctx(
        &self,
        cache_id: &i64,
        data: Vec<Box<OpData>>,
        ctx: Arc<QueryContext>,
        output_target: OutputTarget,
        src_host: String,
        main_pipeline_id: i64,
        plan_id: i64,
    ) -> Result<()> ;
    
    async fn route_data_to_subpipeline(
        &self,
        data: Box<OpData>,
        ctx: ProcessContext<'async_trait>,
    ) -> Result<()>;
    
    async fn route_result(
        &self,
        data: Box<OpData>,
        ctx: ProcessContext<'async_trait>,
    ) -> Result<()>;
    
    async fn collect_result(
        &self,
        data: Box<OpData>,
        ctx: ProcessContext<'async_trait>,
    ) -> Result<()> {
        operator_debug!("collect result");
        GrpcClient::collect_result(
            ctx.op_info.into_grpc_id(),
            vec![*data],
            ctx.op_info.master_name.as_str(),
        )
        .await
    }

    async fn handle_collected_result(
        &self,
        _data: Box<OpData>,
        _ctx: ProcessContext<'async_trait>,
    ) -> Result<()> {
        operator_trace!("handle collecting");
        Ok(())
    }

    async fn exception(&self, _ctx: ProcessContext<'async_trait>) -> Result<()> {
        operator_trace!("got exception");
        Ok(())
    }
}    
```