# Deploying Consul - Notes

- on Kubernetes, Consul can be deployed using the [Consul Helm chart](https://www.consul.io/docs/k8s/helm) or via consul-k8s cli.
- installation is done using the [values.yaml](values.yaml) file to customize it.
- consul is install using the command `consul-k8s install -config-file values.yaml`
- To check the installation status, use `consul-k8s status`
- The resources deployed can be seen using `kubectl get daemonset,statefulset,deployment -n consul`
- consul-k8s must be compatible with the kubernetes cluster version. Check the compatibility matrix [here](https://developer.hashicorp.com/consul/docs/upgrade/k8s/compatibility)
- By default, the installation runs Consul UI on port 8500 forwarded to localhost:8500
- We can insteract with consul using the API, CLI or UI.
