COMPOSE_UP_CMD = docker-compose up --detach webserver
COMPOSE_DOWN_CMD = docker-compose down --remove-orphans

all: run test destroy

run:
	${COMPOSE_UP_CMD}

destroy: 
	${COMPOSE_DOWN_CMD}

test:
	docker-compose run --rm curl run-tests.sh

help:
	docker-compose run --rm curl help.sh

