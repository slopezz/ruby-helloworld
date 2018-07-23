.PHONY: publish

build:
	docker build -t gcr.io/${PROJECT_NAME}/${DOCKER_IMAGE_NAME}:${TRAVIS_COMMIT} .

gcp-auth:
	gcloud auth activate-service-account --key-file "${GOOGLE_APPLICATION_CREDENTIALS}"
	gcloud --quiet config set project ${PROJECT_NAME}
	gcloud --quiet config set container/cluster ${CLUSTER_NAME}
	gcloud --quiet config set compute/zone ${CLOUDSDK_COMPUTE_ZONE}
	gcloud --quiet container clusters get-credentials ${CLUSTER_NAME}

tag-latest:
	docker tag gcr.io/${PROJECT_NAME}/${DOCKER_IMAGE_NAME}:${TRAVIS_COMMIT} gcr.io/${PROJECT_NAME}/${DOCKER_IMAGE_NAME}:latest

gcp-auth-registry: 
	gcloud auth configure-docker

publish:
	docker push gcr.io/${PROJECT_NAME}/${DOCKER_IMAGE_NAME}

deploy: build tag-latest gcp-auth gcp-auth-registry publish
	kubectl config view
	kubectl config current-context
	kubectl set image deployment/${KUBE_DEPLOYMENT_NAME} ${KUBE_DEPLOYMENT_CONTAINER_NAME}=gcr.io/${PROJECT_NAME}/${DOCKER_IMAGE_NAME}:${TRAVIS_COMMIT}
