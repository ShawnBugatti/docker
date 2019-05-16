all: build push
.PHONY: build push

TAG = 7.5.1804

DOCKER_REGISTRY = zx1263526/zx-repo

build:
	docker build -t $(DOCKER_REGISTRY)/centos:$(TAG) .

push:
	docker push $(DOCKER_REGISTRY)/centos:$(TAG)

clean:
	docker rmi $(DOCKER_REGISTRY)/centos:$(TAG)
