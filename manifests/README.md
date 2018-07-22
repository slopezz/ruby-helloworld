Here you will find k8s manifests used to create k8s resources on k8s cluster:

 * Redis-server service: redis-server-service.ymal
 * Redis-server statefulset: redis-server.ymal (with official and public redis:3.2 docker image).
 * Ruby application service: ruby-helloworld-service.yaml (Type LoadBalancer which creates a GCP loadbalancer on port 80 -> 4567)
 * Ruby application deployment: ruby-helloworld.yaml (Container running on port 4567 with initial "latest" image tag)
