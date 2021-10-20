# godevcon
 Docker container as a full-featured VS Code Go development environment 

# Private Registry

Optionale Umgebungsvariablen. Müssen entweder auf dem Hostsystem gesetzt sein, oder in der Console aus welcher VS Code gestarted wird exportiert worden sein!

REGISTRY_PATH 
HTTPS_PROXY
HTTP_PROXY
NO_PROXY

docker build --build-arg REGISTRY_PATH --build-arg  HTTPS_PROXY --build-arg HTTP_PROXY --build-arg NO_PROXY .