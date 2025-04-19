FROM ubuntu:22.04

# Install dev tools and clean up
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
        cmake \
        gdb \
        git \
        openssh-server \
        sudo \
        vim \
        curl && \
    rm -rf /var/lib/apt/lists/*


RUN useradd -ms /bin/bash dev && \
    echo "dev:dev" | chpasswd && \
    usermod -aG sudo dev && \
    echo "dev ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers


RUN mkdir -p /var/run/sshd && \
    echo "PermitRootLogin yes" >> /etc/ssh/sshd_config && \
    echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config


USER dev
WORKDIR /home/dev


EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
