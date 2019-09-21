AZURE_FUNCTIONS_VERSION=2
APP_NAME=python
PYTHON_VERSION=3.6
TAG=$(AZURE_FUNCTIONS_VERSION).$(PYTHON_VERSION)
OWNER=ebrucucen
GIT_TAG=$(OWNER)_$(APP_NAME)_$(TAG)
IMAGE_NAME ?= $(OWNER)/azure-functions-$(APP_NAME):$(TAG)

build:
	docker build -t $(IMAGE_NAME) -f $(APP_NAME)_$(PYTHON_VERSION).dockerfile .

test:
	@docker run --rm -it $(IMAGE_NAME) python --version

shell:
	docker run --rm -it -v ~/.azure:/root/.azure -v $(shell pwd):/opt/app $(IMAGE_NAME) bash

gitTag:
	-git tag -d $(GIT_TAG)
	-git push origin :refs/tags/$(GIT_TAG)
	git tag $(GIT_TAG)
	git push origin $(GIT_TAG)

deploy:
	docker push $(IMAGE_NAME)