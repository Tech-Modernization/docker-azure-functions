AZURE_FUNCTIONS_VERSION=2
PYTHON_VERSION=3.6
TAG = "$(AZURE_FUNCTIONS_VERSION).$(NODE_VERSION)"
IMAGE_NAME ?= ebrucucen/azure-functions-python:$(TAG)

build:
	docker build -t $(IMAGE_NAME) -f node_$(PYTHON_VERSION)x.dockerfile .

test:
	@docker run --rm -it $(IMAGE_NAME) node --version

shell:
	docker run --rm -it -v ~/.azure:/root/.azure -v $(shell pwd):/opt/app $(IMAGE_NAME) bash

gitTag:
	-git tag -d $(TAG)
	-git push origin :refs/tags/$(TAG)
	git tag $(TAG)
	git push origin $(TAG)

deploy:
	docker push $(IMAGE_NAME)