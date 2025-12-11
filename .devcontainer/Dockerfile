FROM fedora:44

# Install required packages
RUN dnf install -y ansible ansible-lint git pip helm kubectl curl tar awk

# Set environment variables for CLI_ARCH
ENV CLI_ARCH=amd64

# Determine the correct architecture
RUN if [ "$(uname -m)" = "aarch64" ]; then CLI_ARCH=arm64; fi

# Download and install Cilium CLI
#RUN CILIUM_CLI_VERSION=$(curl -s https://raw.githubusercontent.com/cilium/cilium-cli/main/stable.txt) \
#    && curl -L --fail --remote-name-all https://github.com/cilium/cilium-cli/releases/download/${CILIUM_CLI_VERSION}/cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum} \
#    && sha256sum --check cilium-linux-${CLI_ARCH}.tar.gz.sha256sum \
#    && tar xzvfC cilium-linux-${CLI_ARCH}.tar.gz /usr/local/bin \
#    && rm cilium-linux-${CLI_ARCH}.tar.gz{,.sha256sum}


RUN pip install kubernetes

RUN ansible-galaxy collection install community.kubernetes