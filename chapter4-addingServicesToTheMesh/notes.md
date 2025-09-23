# Adding Services to the Mesh - Notes

- This chapter uses an example app called "Birdwatcher" to demonstrate how to add services to the mesh.
- The app consists of two microservices:
  - frontend: the UI.
  - backend: the JSON data that is retrieveded via API by the frontend.
- To deploy the app we'll use Kubernets deployments and services.
- The app deployment files are located in the [manifests](manifests/) directory.
- We add apps to the mesh by adding annotations (consul.hashicorp.com/connect-inject: "true") to the K8s service definitions
- When the annotation is added, hence the app is in the mesh, the sidecar proxy (Envoy) is automatically injected into the pod.
- Because of that, the app pod will have two containers: the app container and the Envoy sidecar proxy container.
- It also won't be possible to access the app directly, only via the sidecar proxy.
- A bypass can be done via kubectl by: `kubectl exec deploy/frontend -c frontend -- curl si http://backend/bird`
