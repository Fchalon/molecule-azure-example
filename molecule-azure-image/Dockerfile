FROM ubuntu:22.04

# setup a working environment with python3, azure-cli, and some dev tools
RUN apt-get update && \
    apt-get install -y \
        curl \
        git \
        python3 \
        python3-pip \
        software-properties-common \
        tree \
        vim && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 10 && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 10 && \
    curl -sL https://aka.ms/InstallAzureCLIDeb | bash
#    apt-get install ca-certificates curl apt-transport-https lsb-release gnupg && \
#    mkdir -p /etc/apt/keyrings && \
#    curl -sLS https://packages.microsoft.com/keys/microsoft.asc |gpg --dearmor |  tee /etc/apt/keyrings/microsoft.gpg > /dev/null && \
#    chmod go+r /etc/apt/keyrings/microsoft.gpg && \
#    echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ jammy  main" | tee /etc/apt/sources.list.d/azure-cli.list && \
#    apt-get update && \
#    apt-get install azure-cli=2.51.0~jammy

    
#    curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
#    add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ bionic main" && \
#    apt-get update && \
#    apt-get install -y \
#        azure-cli=2.0.55-1~bionic && \
#    rm -rf /var/lib/apt/lists/*
#    curl -L https://aka.ms/InstallAzureCLIDeb | bash

COPY ./requirement.txt /root/
RUN pip install -r /root/requirement.txt


ENV PYTHONWARNINGS="ignore:Using or importing the ABCs:DeprecationWarning" \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8

# setup the working user
RUN useradd -m -g users --shell /bin/bash molecule
USER molecule
