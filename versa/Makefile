VENDOR=Versa
NAME=FlexVNF
IMAGE_FORMAT=qcow2
IMAGE_GLOB=*.qcow2

# match versions like:
# versa-flexvnf-969d704-20.2.3.qcow2
VERSION=$(shell echo $(IMAGE) | sed -e 's/versa-flexvnf-.*\-\([0-9][0-9]\.[0-9]\.[0-9]\)\.qcow2/\1/')

-include ../makefile-sanity.include
-include ../makefile.include

docker-pre-build:
	-cat cidfile | xargs --no-run-if-empty docker rm -f
	-rm cidfile

docker-build: docker-build-common
	docker run --cidfile cidfile --privileged $(REGISTRY)vr-$(VR_NAME):$(VERSION) --trace 
	docker commit --change='ENTRYPOINT ["/launch.py"]' $$(cat cidfile) $(REGISTRY)vr-$(VR_NAME):$(VERSION)
	docker rm -f $$(cat cidfile)
