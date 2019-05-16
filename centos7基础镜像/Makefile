all: build push
.PHONY: build push

TAG = centos-7.5.1804

DOCKER_REGISTRY = zx1263526/zx-repo

build:
	docker build -t $(DOCKER_REGISTRY):$(TAG) .

push:
	docker push $(DOCKER_REGISTRY):$(TAG)

clean:
	docker rmi $(DOCKER_REGISTRY):$(TAG)
