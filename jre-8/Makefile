VERSION?=alpine3.10
REGISTRY?=g4s8
NAME?=jre-8

release: clean build push clean

build:
	docker build -t $(REGISTRY)/$(NAME):$(VERSION) .

clean:
	docker rm -f $(REGISTRY)/$(NAME):$(VERSION) 2> /dev/null || true

push:
	docker push $(REGISTRY)/$(NAME):$(VERSION)

.PHONY: release clean build push
