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

## Docker Image

The Docker image is built locally using a Dockefile included in this role and then pushed to our Harbor instance.
```bash
docker build -t harbor.status.im/status-im/json-rpc-snoop:0.2 .
docker push harbor.status.im/status-im/json-rpc-snoop:0.2
```

> **Warning:** There is currently no automation pipeline for building this image.