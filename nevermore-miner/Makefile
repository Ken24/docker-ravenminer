IMAGE=nevermore
CONTAINER=nevermore-c

build:
        docker build -t $(IMAGE) .
run:
        docker run -it \
                -v `pwd`/mountpoint:/backup \
                -p 8888:8888 \
                --name=$(CONTAINER) \
                $(IMAGE) /bin/bash
shell:
        docker exec -it $(CONTAINER) /bin/bash
clean: rm
        docker rmi $(IMAGE)
rm:
        docker rm -f $(CONTAINER)
rerun: rm run
stop:
        docker stop $(CONTAINER)
start:
        docker start $(CONTAINER)
restart: stop start