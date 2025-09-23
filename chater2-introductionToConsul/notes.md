# Introduction to Consul - Notes

## Architecture

- A Consul installation is made up of three sets of components:
  - Servers
  - Clients
  - Sidecar proxies
- Sidecar proxies talk to their local clients.
- Clients talk to the servers.
- Ideally there's three to five servers in a Consul datacenter.
- Consul servers and clients are part of the control plane.

## Consul Servers

- Consul servers are Consul database.
- In production, multiple servers should be run. In an odd number (3 or 5) to avoid split-brain scenarios.
- They store data on disk. In K8s they are deployed with persistent volumes and statefulsets.
- On VMs they should be deployed with persisntent disk storage.
- Consensus is achieved using the Raft protocol.
  - Raft does leader election and log replication.
- All writes to Consul go through the leader.
- Consul replicates those writes to the othe Consul servers (aka followers).
- If the leader fails, a new leader is elected from the followers.

## Consul Clients

- Run on every node that runs application workloads.
- Are responsible for detecting the health of services running on their node and of other nodes in the cluster. They, then, report that information to the Consul servers.
- They are also responsible for configuring sidecar proxies running on their node.
- Consul uses SERF to detect failures.
- Failures can be of two types:
  - Node failure: when a node is not reachable.
  - Service failure: when a service is not reachable.
- Consul clients communicate with the servers using a gossip protocol.
- In Kubernetes, Consul clients are deployed as DaemonSets.

## Sidecar proxies

- Each service instance has a dedicated sidecar proxy instance deployed alongside it.
- Sidecar proxies are responsible for intercepting and managing all network traffic to and from the service
- Consul itself is not a proxy, it uses Envoy as the sidecar proxy.
- Envoy has a very low memory and CPU footprint.
- Consul clients configure the sidecar proxies via the gRPC API.
