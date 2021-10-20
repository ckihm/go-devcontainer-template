# available golang images https://hub.docker.com/_/golang
ARG REGISTRY_PATH=
ARG GO_VERSION=1.17
ARG ALPINE_VERSION=3.14

#
# Internen Proxy festlegen
#
ARG HTTPS_PROXY=
ARG HTTP_PROXY=
ARG NO_PROXY=

FROM ${REGISTRY_PATH}${REGISTRY_PATH:+/}golang:${GO_VERSION}-alpine${ALPINE_VERSION}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

ENV HTTP_PROXY=${HTTPS_PROXY} \
    HTTPS_PROXY=${HTTP_PROXY} \
    NO_PROXY=${NO_PROXY}

# Setup user
RUN adduser $USERNAME -s /bin/sh -D -u $USER_UID $USER_GID && \
    mkdir -p /etc/sudoers.d && \
    echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME


ENV GO111MODULE=on

###
# You need to do have a seperate "apk add ca-certicates" in order to run "update-ca-certificates", 
# but once done you can do "apk update ..."
RUN apk add --no-cache \
    ca-certificates
    
# adding CAs so that my curl trusts internal resources AND apk trusts https://dl-cdn.alpinelinux.org behind our proxy
COPY ca/* /usr/local/share/ca-certificates/
RUN update-ca-certificates
###


# Install packages and Go language server
RUN apk add -q --update --progress --no-cache git sudo openssh-client zsh
RUN go get -v golang.org/x/tools/gopls@latest 2>&1

# Setup shell
USER $USERNAME
RUN sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended &> /dev/null
ENV ENV="/home/$USERNAME/.ashrc" \
    ZSH=/home/$USERNAME/.oh-my-zsh \
    EDITOR=vi \
    LANG=en_US.UTF-8
RUN printf 'ZSH_THEME="robbyrussell"\nENABLE_CORRECTION="false"\nplugins=(git copyfile extract colorize dotenv encode64 golang)\nsource $ZSH/oh-my-zsh.sh' > "/home/$USERNAME/.zshrc"
RUN echo "exec `which zsh`" > "/home/$USERNAME/.ashrc"
#USER root