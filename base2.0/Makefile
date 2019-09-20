AZURE_FUNCTIONS_VERSION=2
APP_NAME=base
PYTHON_VERSION=2.0
TAG=$(AZURE_FUNCTIONS_VERSION).$(PYTHON_VERSION)
IMAGE_NAME ?= ebrucucen/azure-functions-base:$(TAG)

build:
	docker build -t $(IMAGE_NAME) -f base_$(PYTHON_VERSION).dockerfile .

test:
	@docker run --rm -it $(IMAGE_NAME) base --version

shell:
	docker run --rm -it -v ~/.azure:/root/.azure -v $(shell pwd):/opt/app $(IMAGE_NAME) bash

gitTag:
	-git tag -d $(TAG)
	-git push origin :refs/tags/$(TAG)
	git tag $(TAG)
	git push origin $(TAG)

deploy:
	docker push $(IMAGE_NAME)