DATA_CONTAINER=grails_data

all: run

build:
	sudo docker build -t shaneburkhart/dev:grails .

run:
	if sudo docker ps -a | grep ${DATA_CONTAINER}; then \
		echo "${DATA_CONTAINER} already exists."; \
		echo "Using existing container."; \
	else \
		sudo docker run \
			-v /home \
			--name ${DATA_CONTAINER} \
			dockerfile/ubuntu \
			true; \
	fi
	sudo docker run -it --rm \
	    --volumes-from ${DATA_CONTAINER} \
	    -v /run/docker.sock:/run/docker.sock \
	    -v /home/shane/.ssh:/root/.ssh \
	    shaneburkhart/dev:grails
