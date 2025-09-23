# Ingress Gateways - Notes

- As Consul is secure by default, we need to explicitly allow ingress traffic to reach our services. This is done by configuring an ingress gateway.
- The ingress gateway sets the necessary authorization for the services to be reachable from outside the mesh.
- Under the hood the ingress gateway is just another Envoy proxy, but it is configured to allow incoming traffic.
- The ingress gateway is deployed via the [values.yaml](./chapter5-ingressGateways/values.yaml) file.
- Consul uses Config Entries allow us to configure the serice mesh dynamically.
- Config entries don't need us to run the `consul-k8s` tool or reloading Consul, they take effect immediately.
- They are organised into kinds:
  - Ingress Gateway
  - Proxy Defaults: configure defaults for all proxies in the mesh.
  - Service intentions: configure intentions. Which are authorization rules in Consul.
  - Service router, resolver and splitter: configure advanced traffic routing.
- In K8s, config entries are defined as custom resources (CRDs). These are YAML files that are applied via `kubectl apply -f <file>`.
- example of config entries can be found [here](config-entries/).

## Configuring ingress gateway

- Ingress gateways can use multiple listeners (ports).
- These listeners support the following settings:
  - Port
  - Protocol
  - TLS
  - Routing Configuration - which service to route to.
