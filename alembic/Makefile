include env_make
VERSION ?= 01

REPO = alembic_migration
NAME = alembic

.PHONY: build push debug run start stop rm release

build:
	docker build -t $(REPO):$(VERSION) .

push:
	docker push $(REPO):$(VERSION)

debug:
	docker run --rm --name $(NAME) -i -t $(VOLUMES) $(REPO):$(VERSION) /bin/bash

run:
	docker run --rm --name $(NAME) $(VOLUMES) $(ENV) $(REPO):$(VERSION)

start:
	docker run -d --name $(NAME) $(PORTS) $(VOLUMES) $(ENV) $(REPO):$(VERSION)

stop:
	docker stop $(NAME)

rm:
	docker rm $(NAME)

release: build
	make push -e VERSION=$(VERSION)

default: build
and don’t forget to place an env_make file next to your Makefile that is ignored by the VCS:


VOLUMES = -v ${PWD}/versions:/usr/src/app/migration/versions
