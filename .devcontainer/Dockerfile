FROM golang:1.25-trixie AS golang
FROM debian:trixie

WORKDIR /app
ENV DEBIAN_FRONTEND="noninteractive"
ENV PATH="$PATH:/usr/local/go/bin"
ENV GOBIN="/usr/local/go/bin"

# Install golang from docker image
COPY --from=golang /usr/local/go /usr/local/go

# Install system dependencies
RUN mkdir -p /tmp/dl && cd /tmp/dl && \
    # Install apt dependencies
    apt update && \
    apt install -y wget curl zip unzip p7zip-full git tree && \
    # Install task
    wget --no-verbose https://github.com/go-task/task/releases/download/v3.44.1/task_linux_amd64.tar.gz && \
    tar -xzf task_linux_amd64.tar.gz && \
    mv ./task /usr/local/bin/task && \
    # Install golangci-lint
    wget --no-verbose https://github.com/golangci/golangci-lint/releases/download/v2.4.0/golangci-lint-2.4.0-linux-amd64.tar.gz && \
    tar -xzf golangci-lint-2.4.0-linux-amd64.tar.gz && \
    mv ./golangci-lint-2.4.0-linux-amd64/golangci-lint /usr/local/bin/golangci-lint && \
    # Clean up temp dir
    cd /app && rm -rf /tmp/dl && \
    # Clean up apt cache
    rm -rf /var/lib/apt/lists/*

##############
# START HERE #
##############

# Add the startup script on every bash session
RUN rm -rf /root/.bashrc
COPY .devcontainer/.bashrc /root/.bashrc

# Command just to keep the container running
CMD ["sleep", "infinity"]
