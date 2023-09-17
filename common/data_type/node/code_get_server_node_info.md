#1.get_server_node_info

```
get_server_node_info
--SERVER_NODE.get_or_init(|| {lambda})
--lambda
----let mgr = SystemConfigManager::instance();
----let name = mgr.get_value_into::<String>(config_item::NODE_NAME, &ConfigType::Config);
        let ip_address =
            mgr.get_value_into::<String>(config_item::NODE_IP_ADDRESS, &ConfigType::Config);
        let node_id = mgr.get_value_into::<u32>(config_item::NODE_NODE_ID, &ConfigType::Config);
        let cluster_id =
            mgr.get_value_into::<u32>(config_item::NODE_CLUSTER_ID, &ConfigType::Config);

        let port = mgr.get_value_into::<u32>(config_item::NODE_INTERNAL_PORT, &ConfigType::Config);
        let raft_port =
            mgr.get_value_into::<u32>(config_item::NODE_PARTITION_RAFT_PORT, &ConfigType::Config);
        let compute_node_type = NodeType::Compute;

        let label = compute_node_type.as_str_name().to_string();
        let node_type = compute_node_type as i32;

        NodeInfoMsg {
            name,
            ip_address,
            node_id,
            cluster_id,
            port,
            raft_port,
            label,
            last_report_time: "".to_string(),
            node_status: NodeStatus::Online as i32,
            node_type,
        }
```