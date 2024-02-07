FROM ubuntu:18.04

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
    curl -sSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ bionic main" && \
    apt-get update && \
    apt-get install -y \
        azure-cli=2.0.55-1~bionic && \
    rm -rf /var/lib/apt/lists/*

# install ansible, ansible[azure], and molecule
COPY files/setup /root/setup
RUN pip install -r /root/setup/requirements.txt

# ignore the collections.abc deprication warnings and set lang vars to UTF-8
ENV PYTHONWARNINGS="ignore:Using or importing the ABCs:DeprecationWarning" \
    LC_ALL=C.UTF-8 \
    AZURE_SECRET=KFF8Q~XrhOPsbxmu9x7vICqDHWJgZTaBSL4XMdcL \
    AZURE_TENANT=d1c719f7-cc48-4f9f-83ec-f706a2a940fe \
    AZURE_SUBSCRIPTION_ID=19a7ed62-f51f-4e53-b3ea-6ba9a63f17fe \
    AZURE_CLIENT_ID=56d94015-47e4-4401-a4a5-5ab03a6a5e7c \
    AZURE_RESOURCE_GROUP=rg-fabrykpoc1-core-kcl-eastus-002 \
    LANG=C.UTF-8

LABEL molecule-azure.ansible.version=2.7.6 \
      molecule-azure.azure-cli.version=2.0.55 \
      molecule-azure.molecule.version=2.19.0

# setup the working user
RUN useradd -m -g users --shell /bin/bash molecule
USER molecule

WORKDIR /playbook
