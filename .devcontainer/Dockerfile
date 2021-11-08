ARG VERSION="latest"
ARG REGISTRY_PATH=""

#FROM ${REGISTRY_PATH}${REGISTRY_PATH:+/}ckihm/go-build:${VERSION}
FROM ckihm/go-build

# Setting the ENTRYPOINT to docker-init.sh will configure non-root access 
# to the Docker socket. The script will also execute CMD as needed.
ENTRYPOINT [ "/usr/local/share/docker-init.sh" ]
CMD [ "sleep", "infinity" ]