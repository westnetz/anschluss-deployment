.DEFAULT_GOAL := help

.PHONY: help
help:
	@grep -E '^[\.a-zA-Z0-9_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-30s\033[0m %s\n", $$1, $$2}'

CT ?= docker-compose run --rm ct
.PHONY: config
config: ## Transpiles Cloud Linux YML to Ignition JSON
	@if grep -q GITCRYPT deployment-key.pgp; then \
		echo "Run git-crypt unlock first" >&2; \
		exit 1; \
	fi
	$(CT) \
		-files-dir /host \
		-pretty \
		-strict \
		< config.yml \
		> config.json

.PHONY: clean
clean: ## Cleans up files which are build artefacts
	rm -f config.json
