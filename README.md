# ruby-helloworld

The application is running on a Google Cloud Kubernetes Cluster. It consist on:

 * A K8s StatefulSet with a single redis instance (replica = 1).
 * A K8s Deployment with a simple ruby application connection to a Redis server (redis.ping) usign ENV variables (replica=2).

Ruby application dockerfile can be located at [app](app/)

K8s manifest can be located at [manifests](manifest/)

In order to update the application message at hello-world.rb, you need to create a branch and do a PR to master (protected branch).

Once a PR is accepted and merged into master protected branch, a Travis CI is executed, building a new docker image, pushing it to private docker registry on GCP, and performing a kubernetes rolling update of ruby-helloworld deployment.
