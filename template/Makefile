.DEFAULT_GOAL := help
.PHONY: help setup test lint format update clean

help: ## Show available commands
	@grep -E '^[a-z]+:.*## ' $(MAKEFILE_LIST) | awk 'BEGIN {FS = ":.*## "}; {printf "  \033[36m%-8s\033[0m %s\n", $$1, $$2}'

setup: ## Install dependencies and git hooks
	uv sync
	uv run pre-commit install

test: ## Run unit tests
	uv run pytest

lint: ## Run all pre-commit hooks on every file
	uv run pre-commit run --all-files

format: ## Format code and auto-fix lint issues
	uv run ruff format
	uv run ruff check --fix

update: ## Upgrade locked dependencies and pre-commit hooks
	uv lock --upgrade
	uv run pre-commit autoupdate

clean: ## Remove caches and build artifacts
	rm -rf .ruff_cache build dist
	find . -type d -name __pycache__ -prune -exec rm -rf {} +
