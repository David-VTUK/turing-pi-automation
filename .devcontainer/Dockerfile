FROM fedora:44

# Install required packages
RUN dnf install -y ansible ansible-lint git pip helm kubectl curl tar awk jq openssl

# Set environment variables for CLI_ARCH
ENV CLI_ARCH=amd64

# Determine the correct architecture
RUN if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi

# Download and install Cilium CLI
RUN CILIUM_CLI_VERSION=$(curl -s https://api.github.com/repos/cilium/cilium-cli/releases/latest | grep '"tag_name":' | awk -F '"' '{print $4}') \
    && curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum} \
    && sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum \
    && tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin \
    && rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}

# Download and install the tpi CLI
RUN curl -sSL https://github.com/turing-machines/tpi/releases/download/1.0.7/tpi-x86_64-unknown-linux-gnu.tar.gz -o /tmp/tpi.tar.gz && \
    mkdir -p /tmp/tpi_extracted && \
    tar -xzf /tmp/tpi.tar.gz -C /tmp/tpi_extracted && \
    mv /tmp/tpi_extracted/usr/bin/tpi /usr/local/bin/tpi && \
    chmod +x /usr/local/bin/tpi && \
    rm -rf /tmp/tpi.tar.gz /tmp/tpi_extracted

# Download and install the Talosctl CLI
RUN curl -sL https://talos.dev/install | sh

RUN pip install kubernetes

RUN ansible-galaxy collection install community.kubernetes