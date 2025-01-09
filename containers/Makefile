UNISON_IMAGE_NAME ?= localhost/unison
UNISON_VERSION ?= latest
UNISON_REPO_VERSION := $(if $(filter latest,$(UNISON_VERSION)),$(shell curl -s https://api.github.com/repos/bcpierce00/unison/releases/latest | jq -r .tag_name),$(UNISON_VERSION))
UNISON_CURRENT_VERSION := $(subst v,,$(UNISON_REPO_VERSION))
CONTAINER_BUILD_CONTEXT ?= .

unison:
	buildah build \
		-f ubuntu-source/Containerfile \
		--build-arg UNISON_IMAGE_NAME=${UNISON_IMAGE_NAME} \
		--build-arg UNISON_VERSION=${UNISON_CURRENT_VERSION} \
		--format oci \
		--layers=true \
		--target unison \
		--tag ${UNISON_IMAGE_NAME}:${UNISON_VERSION} \
		--tag ${UNISON_IMAGE_NAME}:${UNISON_CURRENT_VERSION} \
	${CONTAINER_BUILD_CONTEXT}

ubuntu-24.04:
	buildah build \
		-f ubuntu-24.04/Containerfile \
		--format oci \
		--layers=true \
		--target unison \
		--tag ${UNISON_IMAGE_NAME}:ubuntu-24.04 \
	${CONTAINER_BUILD_CONTEXT}

.PHONY: runtime ubuntu-24.04