.PHONY : test run destroy clean test_web test_db client help
.DEFAULT_GOAL := help
test: test_web test_db ## runs all tests

build:  ## since we have no custom images, this will just pull the latest containers
	docker pull nginx
	docker pull percona

run: ## deploys the application
	docker-compose up -d webserver
	docker-compose up -d database

	# TODO add a healthcheck to the app so we don't have this awful wait
	sleep 30

	docker-compose run --rm data_load

destroy: ## shuts everything down and cleans up the env
	@echo "Shutting everything down..."
	docker-compose down --remove-orphans
	make clean

clean: ## resets env
	@echo "Cleaning Database directory"
	rm -rf ./data/*

test_web: ## runs web tests
	@echo "Running Web Tests..."
	make -f ./test.web.Makefile all

test_db: ## runs database tests
	# @echo "seeding the database"
	# docker-compose up -d dataload
	@echo "Running DB Tests..."
	make -f ./test.db.Makefile all

client: ## runs a container as an interactive terminal
	docker-compose run --rm client bash

help: ## prints this message
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'
