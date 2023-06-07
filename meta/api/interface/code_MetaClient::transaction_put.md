#1.MetaClient::transaction_put

```
MetaClient::transaction_put
--let mut condition = vec![];
--let mut execution = vec![];

--for (key, value) in kvs.iter() {
            condition.push(etcd_client::Compare::value(
                key.as_str(),
                etcd_client::CompareOp::NotEqual,
                value.as_str(),
            ));
            execution.push(etcd_client::TxnOp::put(key.as_str(), value.as_str(), None));
        }

--// transaction
--let txn = etcd_client::Txn::new().and_then(execution);

--self.etcd_client.clone().txn(txn).await?;

```