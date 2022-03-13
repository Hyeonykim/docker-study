ifndef VERBOSE
.SILENT:
endif

# import config
cnf ?= config.env
include $(cnf)
export $(shell sed 's/=.*//' $(cnf))


.PHONY: help

help: ## This help
		awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST);

build_image:
	echo "[CMD] docker build . -t ${imageName} --no-cache"
	docker build . -t ${imageName} --no-cache

remove_container:
	echo "[CMD] docker container inspect ${containerName}"
	docker container inspect ${containerName} > /dev/null
	if [ $$? -eq 0 ] ; then \
		echo "[CMD] docker stop ${containerName}"; \
		docker stop ${containerName}; \
		echo "[CMD] docker container rm ${containerName}"; \
		docker container rm ${containerName}; \
	fi

build: build_image ## Build

reload: remove_container ## Reload coitainer
	echo "[CMD] docker run -d --name ${containerName} ${imageName}"
	docker run -d --name ${containerName} ${imageName}

shell: ## Connect to shell
	echo "[CMD] docker exec -it ${containerName} bash"
	docker exec -it ${containerName} bash

clean: remove_container ## Remove container
	# clean unused container
	#echo "[CMD] yes y	| docker container prune"
	#yes y	| docker container prune

