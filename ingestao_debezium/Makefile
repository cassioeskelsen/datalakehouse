#!make

export PYTHON=python

default: build_debezium

build_debezium:
	DOCKER_BUILDKIT=1 docker image build --tag debezium:latest --build-arg SOURCE_FOLDER=api --no-cache  -f debezium-server/Dockerfile .

run_debezium:
	docker run -it --name debezium_container -p 8080:8080 -v $PWD/conf:/debezium/conf -v $PWD/data:/debezium/data debezium/server

stop_debezium:
	docker rm --force debezium_container

create_config_from_properties:
	kubectl create configmap debezium-server-config --from-file=./conf/application.properties --namespace data-ingestion