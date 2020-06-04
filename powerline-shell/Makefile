all: help

help:
	@echo ""
	@echo "-- Help Menu"
	@echo ""
	@echo "   1. make prep             - do prep work for all images"
	@echo "   2. make build            - build all images"
	@echo "   3. make pull             - pull all images"
	@echo "   4. make clean            - remove all images"
	@echo ""

prep:
	@./build-opt.sh

build: prep
	@docker build --tag=christophebedard/images:powerline-shell .

pull:
	@docker pull christophebedard/images:powerline-shell

clean:
	@ rm -rf _opt
	@docker rmi -f christophebedard/images:powerline-shell
