build:
		DOCKER_BUILDKIT=1 docker buildx build \
		--platform linux/amd64,linux/arm64 \
		--build-arg TELEGRAF_VERSION=1.32.2 \
		--build-arg VERSION=9.9.9 \
		-t telegraf-qnap:9.9.9 \
		--output="type=image" \
		--no-cache \
		--load \
		.