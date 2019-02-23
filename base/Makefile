NAME=pcl_base
VERSION=1.0

build:
	docker build -t $(NAME):$(VERSION) .

restart: stop start

start:
	docker run -itd \
		-p 8888:8888 \
		-p 6006:6006 \
		--privileged \
		--name $(NAME) \
		$(NAME):$(VERSION) bash

contener=$(shell `docker ps -a -q`)
image=$(shell `docker images | awk '/^<none>/ { print $$3 }'`)

clean:
	@if [ "$(image)" != "" ] ; then \
		docker rmi $(image); \
	fi
	@if [ "$(contener)" != "" ] ; then \
		docker rm $(contener); \
	fi

stop:
	docker rm -f $(NAME)

attach:
	docker exec -it $(NAME) /bin/bash

logs:
	docker logs $(NAME)