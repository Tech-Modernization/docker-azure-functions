# docker-azure-functions
🐳 Containerised Azure Functions Node to run serverless workloads


## Usage
Run as a command using `node` as entrypoint:

    docker run --rm --entrypoint node contino/azure-functions-node --version

Run as a shell and mount `.azure` folder and current directory as volumes:

    docker run --rm -it -v ~/.azure:/root/.azure -v $(pwd):/opt/app contino/azure-functions-node bash

Using docker-compose:
```
version: '3.4'
services:
    sls:
      image: amaysim/serverless:1.49.0
      env_file: .env
      volumes:
      - ~/.azure:/root/.azure
      - .:/opt/app

    azure-nodejs8:
        image: contino/azure-functions-node:0.2.8
        working_dir: /var/task/azure-nodejs8
        volumes:
        - .:/var/task
    azure-nodejs10:
        image: ebrucucen/azure-functions-node:0.2.10
        working_dir: /var/task/azure-nodejs10
        volumes:
        - .:/var/task
    azure-python3.6:
        image: contino/azure-functions-python:3.6
        working_dir: /var/task/azure-nodejs8
        volumes:
        - .:/var/task
    azure-python3.7:
        image: ebrucucen/azure-functions-python:3.7
        working_dir: /var/task/azure-nodejs10
        volumes:
        - .:/var/task```

And it could be used in a Makefile: 
```
BUILDER=docker-compose -f ../docker-compose.yml run --rm $(RUNTIME)
SLS=docker-compose -f ../docker-compose.yml run --rm -w /opt/app/$(RUNTIME) sls

clean: ../.env
	$(BUILDER) make _clean

build: ../.env
	$(BUILDER) make _build

deploy: ../.env
	$(SLS) deploy --package .serverless
```

## Build 
For new versions, create a folder with a Makefile and dockerfile.
Set the `AZURE_FUNCTIONS_VERSION`  and `NODE_VERSION` in both `Makefile` and `DockerFile`. 
The `dockerfile` referenced Node version in this line: `https://deb.nodesource.com/setup_**10**.x`
    make build
    make test
    make deploy
Integrate into your ci pipeline

## Related Projects

- [docker-terraform](https://github.com/contino/docker-terraform)
- [docker-aws-cli](https://github.com/contino/docker-aws-cli)