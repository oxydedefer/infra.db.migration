# include env_make
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

upgrade_head:
	docker exec $(NAME) alembic upgrade head

upgrade:
	docker exec $(NAME) alembic upgrade $(REVISION)

downgrade:
	docker exec $(NAME) alembic downgrade $(REVISION)

revision:
	docker exec $(NAME) alembic revision -m  "$(MESSAGE)"

run:
	docker run --rm --name $(NAME) $(VOLUMES) $(ENV) $(REPO):$(VERSION)

start:
	docker start --name $(NAME)

stop:
	docker stop $(NAME)

rm:
	docker rm $(NAME)

release: build
	make push -e VERSION=$(VERSION)

default: build


VOLUMES = -v ${PWD}/versions:/usr/src/app/migration/versions
