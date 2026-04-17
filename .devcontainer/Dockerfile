FROM fedora:45

# Install required packages
RUN dnf install -y ansible ansible-lint git pip helm kubectl curl tar awk podman podman-docker jq

# Set environment variables for CLI_ARCH
ENV CLI_ARCH=amd64

# Determine the correct architecture
RUN if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi

# Download and install Cilium CLI
RUN curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/latest/download/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum} \
    && sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum \
    && tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin \
    && rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}

RUN pip install kubernetes

RUN ansible-galaxy collection install community.kubernetes