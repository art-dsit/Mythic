BINARY_NAME=mythic-cli
LOCAL_PATH=$(shell pwd)
BUILDER_IMAGE=ghcr.io/its-a-feature/mythic_cli:v3.3.0.14
CONTAINER_NAME=mythic-cli-temp
.PHONY: default
default: build_linux ;

# pull in build and env options from global settings
-include ../build.env
-include ../.env

export

copy_binary_linux:
        @docker run --name ${CONTAINER_NAME} ${BUILDER_IMAGE} sh -c "cp /mythic-cli_linux /copy_file/mythic-cli-linux"
        @docker container cp ${CONTAINER_NAME}:/copy_file/mythic-cli-linux ./mythic-cli
        @docker rm ${CONTAINER_NAME}
        chmod +x ./mythic-cli

copy_binary_macos:
        @docker run --name ${CONTAINER_NAME} ${BUILDER_IMAGE} sh -c "cp /mythic-cli_macos /copy_file/mythic-cli-macos"
        @docker container cp ${CONTAINER_NAME}:/copy_file/mythic-cli-macos ./mythic-cli
        @docker rm ${CONTAINER_NAME}
        chmod +x ./mythic-cli

build_local:
       cd src && go build -o ../../mythic-cli .

build_linux_docker:
        docker build -t mythic-cli-builder -f Dockerfile .
        @docker run --name ${CONTAINER_NAME} mythic-cli-builder sh -c "cp /mythic-cli_linux /copy_file/mythic-cli-linux"
        @docker container cp ${CONTAINER_NAME}:/copy_file/mythic-cli-linux ./mythic-cli
        @docker rm ${CONTAINER_NAME}
        chmod +x ./mythic-cli

build_macos_docker:
        docker build -t mythic-cli-builder -f Dockerfile .
        @docker run --name ${CONTAINER_NAME} mythic-cli-builder sh -c "cp /mythic-cli_macos /copy_file/mythic-cli-macos"
        @docker container cp ${CONTAINER_NAME}:/copy_file/mythic-cli-macos ./mythic-cli
        @docker rm ${CONTAINER_NAME}
        chmod +x ./mythic-cli

build_linux: copy_binary_linux
build_macos: copy_binary_macos
