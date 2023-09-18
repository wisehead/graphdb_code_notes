#1.GrpcCommon::build_grpc_request

```
GrpcCommon::build_grpc_request
--let mut tonic_request = tonic::Request::new(msg);

--tonic_request.set_timeout(Duration::from_secs(timeout));

--if let Some(request_id) = request_id {
            tonic_request
                .metadata_mut()
                .insert("x-request-id", MetadataValue::try_from(request_id).unwrap());
        }
--let parent_ctx = tracing::Span::current().context();

--global::get_text_map_propagator(|propagator| {
            propagator.inject_context(&parent_ctx, &mut MetadataMap(tonic_request.metadata_mut()));
        });
```