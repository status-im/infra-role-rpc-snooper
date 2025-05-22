# Description

This role configures [json_rpc_snoop](https://github.com/ethDreamer/json_rpc_snoop), a tool for monitoring RPC calls between Ethereum clients. It works as a proxy that logs all JSON-RPC requests and responses, particularly useful for debugging communications between Beacon nodes and Execution clients.

## Installation

```yaml
- name: infra-role-rpc-snooper
  src: git@github.com:status-im/infra-role-rpc-snooper.git
  scm: git
```

# Configuration

The main settings to adjust are the container name, port, and target Ethereum RPC endpoint:

```yaml
rpc_snooper_service_name: 'rpc-snooper-stable'
rpc_snooper_service_port: 9552
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

## Build

Ensure you have cargo installed and in your PATH (the easiest way is to visit https://rustup.rs/)

make

```bash
cargo build --release
```

> **Warning:** There is currently no automation pipeline for building this image. The binaries used are built locally and pushed to this repo.