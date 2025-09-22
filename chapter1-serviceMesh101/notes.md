# Service mesh 101 - Notes

![Service stack](./images/service_stack.svg)

- The figure above shows a typical software stack. Service mes is considered to be a middleware.
- A service mesh is an infrastructure layer that enables the control of the network communication of the workloads from a single control plane.
- Service mesh is not part of your services, it is deployed and operated independently.
- Service mesh controls the traffic entering and leaving a microservice, database or anything else that does network communication.
- A sevice mesh mesh has complete control over _all traffic_ entering and leaving the services.

## How service mesh works

- A service mesh is made up of sidecar proxies and the control plane.
- Each instance of a service must be deployed with it's own local proxy (sidecar proxy).
- Sidecar proxies enable control of service traffic without afecting the service itself.
- The control plane manages and configures the proxies to route traffic.
- The control plane is where most of the complex logic of the service mesh lives: it must watch for services starting and stopping, sign and distribute certificates, reconfigure proxies, and more.
- Sidecar proxies receive configuration from the control plane detailing which actions to perform non traffic and they execute those actions.

## Why use a service mesh

- A service mesh provide features in four areas:
  - Traffic control
  - Security
  - Observability
  - Reliability
- It provides these features to every service and workload _without modifying the service code_.

### Security

- One of the primary reasons companies deploy service meshes is to secure their networks. Tipycally by encrypting traffic between services.
- It also does that by implementing authentication and authorization policies.
- A service mesh does that by using mutual TLS (mTLS) to encrypt traffic between services via the sidecar proxies without any changes to the services themselves.

### Observability

- It's the ability to understand what's happening to your services while they are running.
- Capturing observability data is a perfect job for service meshes because all requests flow through the sidecar proxies.

### Reliability

- In distributed systems, there's often something failing.
- Making reliable distributed systems often means reducing failures (by implementing health checks) or handling failures (retrying requests) when possible gracefully.
- Again, both of these are done via the sidecar proxies without any changes to the services themselves.

### Traffic control

- It's about controlling where traffic between services flows.
- It solves many problems:
  - Enable canary deployments
  - Monolith to microservices migrations
  - Multi-cluster failover

## When to use a service mesh

- Service meshes can introduce complexity and network latency. It alsos increase the use of compute resources for the sidecar proxies.
- Because of that for a service mesh to be worth it, it must provide a lot of value for the organization.
