PYTHON  ?= python
SHELL   := /bin/bash
PACKAGE =  cloud_foundation_toolkit

help:
	@echo "cft-prerequisites         Installs prerequisites for CFT python utility development"
	@echo "cft-venv                  Creates the virtual environment called 'venv' for development"
	@echo "cft-clean-venv            Deletes the development environment"
	@echo "cft-test                  Runs all unit tests from outside of the venv (for CI tools)"
	@echo "cft-test-venv             Runs all unit tests from withing the venv (for active development)"
	@echo "template-prerequisites    Install prerequisites for template development"
	@echo "build                     Builds the package"
	@echo "install                   Installs the package system wide"
	@echo "uninstall                 Uninstalls the package"
	@echo "clean                     Cleanup build/test/cache files"


.ONESHELL:
.PHONY: cft-prerequisites cft-venv cft-clean-venv cft-test cft-test-venv template-prerequisites

prerequisites:
	${PYTHON} -m pip install -r requirements/prerequisites.txt

cft-venv:
	${PYTHON} -m tox -e venv

cft-clean-venv:
	rm -rf venv

cft-test:
	${PYTHON} -m tox -- -x tests/unit

cft-test-templates:
	${PYTHON} -m tox -- -x tests/templates

cft-test-venv:
	${PYTHON} -m pytest -v

template-prerequisites:
	rm -rf bats && git clone https://github.com/sstephenson/bats.git && ./bats/install.sh venv && rm -rf bats

build:
	${PYTHON} setup.py sdist bdist_wheel

install:
	${PYTHON} -m pip install dist/${PACKAGE}-$$(cat VERSION)-py2.py3-none-any.whl

uninstall:
	${PYTHON} -m pip uninstall ${PACKAGE} -y

clean:
	find src/${PACKAGE} \( -path '*__pycache__/*' -o -name __pycache__ \) -delete
	find tests \( -path '*__pycache__/*' -o -name __pycache__ \) -delete
	rm -rf build dist *.egg-info .cache .eggs .coverage
