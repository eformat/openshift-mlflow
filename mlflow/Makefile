# Image URL to use all building/pushing image targets
REGISTRY ?= quay.io
REPOSITORY ?= $(REGISTRY)/eformat

MLFLOW_VERSION ?= 2.22.0
PYTHON_TAG ?= 9.6-1747332104
PYTHON_IMG ?= registry.access.redhat.com/ubi9/python-39:$(PYTHON_TAG)
MLFLOW_IMG := $(REPOSITORY)/mlflow:$(MLFLOW_VERSION)

podman-login:
	@podman login -u $(DOCKER_USER) -p $(DOCKER_PASSWORD) $(REGISTRY)

podman-build-mlflow:
	podman build --from ${PYTHON_IMG} --build-arg MLFLOW_VERSION=$(MLFLOW_VERSION) . -t ${MLFLOW_IMG} -f Dockerfile

podman-push-mlflow: podman-build-mlflow
	podman push ${MLFLOW_IMG}

build: podman-build-mlflow

push: podman-push-mlflow
