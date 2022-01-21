build:
	docker image build \
		--tag homebrew-env \
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
		--publish 8887:8887 \
		homebrew-env

