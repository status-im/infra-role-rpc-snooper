# Description

This role configures [json_rpc_snoop](https://github.com/ethDreamer/json_rpc_snoop), a tool for monitoring RPC calls between Ethereum clients. It works as a proxy that logs all JSON-RPC requests and responses, particularly useful for debugging communications between Beacon nodes and Execution clients.

The image used by default is [harbor.status.im/status-im/json-rpc-snoop](https://harbor.status.im/harbor/projects/status-im/repositories/json-rpc-snoop/artifacts-tab).

## Installation

```yaml
- name: infra-role-rpc-snooper
  src: git@github.com:status-im/infra-role-rpc-snooper.git
  scm: git
```

# Configuration

The main settings to adjust are the container name, port, and target Ethereum RPC endpoint:

```yaml
rpc_snooper_cont_name: 'rpc-snooper-stable'
rpc_snooper_cont_port: 9552
rpc_snooper_el_port: 8552
```

For better log readability, you can suppress noisy method calls or paths:
```yaml
rpc_snooper_suppress_methods:
  - "eth_sendConsensusMessage"
  - "eth_testConsensusFallback"
  - "eth_syncing"

rpc_snooper_suppress_paths:
  - "/engine/v1/events"
```
