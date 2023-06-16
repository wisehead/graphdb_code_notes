#1.Config::get

```
Config::get
--INSTANCE.get_or_init
----let mut config_path = "./config.toml".to_string();
----if let Ok(p) = std::env::var("ARCGRAPH_CONFIG") {
                    config_path = p
----} else if let Some(p) = path {
                    config_path = p.to_string();
----let mut cfg_from_file = Config::from_config_file(&config_path).unwrap();
----std::thread::spawn(move || {Config::watch(config_path);});

----if let Ok(env_arg) = std::env::var("POD_NAME") {
------let splited: Vec<&str> = env_arg.split('-').collect();
------let prefix_name = splited[0];
------if let Ok(index) = from_str::<i32>(splited.last().unwrap()) {
--------// pod_name.serviec_name as ip_address
                        let service_name: String =
                            if let Ok(service) = std::env::var("SERVICE_NAME") {
                                service
                            } else {
                                "arcgraph-svc".to_string()
                            };

                        let index = index + 1;
                        cfg_from_file.node.name = format!("computing-{:02}", index);
                        cfg_from_file.node.machine_id = index;
                        cfg_from_file.node.node_id = index;
                        let ip_address = format!("{}.{}", &env_arg, &service_name);
                        cfg_from_file.node.ip_address = ip_address.clone();
                        cfg_from_file.meta.ip_address = ip_address;
                        let meta_raft_port = if cfg_from_file.node.port.len() >= 2 {
                            cfg_from_file.node.port[2]
                        } else {
                            5001
                        };

                        // dynamic reset meta raft peer ip address
                        cfg_from_file.raft_peer[0].address =
                            format!("{}-0.{}:{}", prefix_name, &service_name, meta_raft_port);
                        cfg_from_file.raft_peer[1].address =
                            format!("{}-1.{}:{}", prefix_name, &service_name, meta_raft_port);
                        cfg_from_file.raft_peer[2].address =
                            format!("{}-2.{}:{}", prefix_name, &service_name, meta_raft_port);
----// reset etcd address
----if let Ok(env_arg) = std::env::var("ETCD_ADDR") {
                    let address: Vec<String> =
                        env_arg.split(',').map(|item| item.to_string()).collect();
                    cfg_from_file.meta.endpoints = Box::new(address);
                }

----// reset pd address
----if let Ok(env_arg) = std::env::var("PD_ADDR") {
                    let address: Vec<String> =
                        env_arg.split(',').map(|item| item.to_string()).collect();
                    cfg_from_file.tikv.pd_address = Box::new(address);
                }

----// rest opensearch address
----if let Ok(env_arg) = std::env::var("OPENSEARCH_ADDR") {
                    cfg_from_file.search_config.opensearch_url = env_arg;
```