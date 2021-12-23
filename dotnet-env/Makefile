build:
	docker buildx build \
		--tag dotnet-env \
		--file Dockerfile \
		--build-arg UID=$(shell id -u) \
		--build-arg GID=$(shell id -u) \
		${PWD}

run:
	docker container run \
		--init \
		--interactive \
		--tty \
		--rm \
		--mount type=bind,src=${PWD},dst=/workspace \
		--publish 8889:8889 \
		dotnet-env

