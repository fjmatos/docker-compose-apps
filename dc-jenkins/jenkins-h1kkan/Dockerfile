
#FROM h1kkan/jenkins-docker:2.303.1
FROM h1kkan/jenkins-docker:2.319.3

LABEL Owner="xabier.matos@gmail.com"

# if we want to install via apt

USER root

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update &&  \
    apt-get install -y apt-utils sshpass vim unzip wget dialog
RUN apt-get install -y sudo


# Cambiamos la zona horaria del contenedor
ENV TZ=Europe/Madrid
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


# Añadimos el repo Debian Testing para instalar python 3.8 ya que Debian Stable esta python  3.6
#
## RUN echo "deb http://ftp.de.debian.org/debian testing main" >> /etc/apt/sources.list

# Desactivo esta seccion porque me da fallo con las keys
## RUN apt install -y gnupg2
#RUN gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 04EE7237B7D453EC


# Instalamos python3 pero es necesario desactivar el repor Inmmediate

## RUN apt-get update
## RUN apt-get -t testing install -y python3 -o APT::Immediate-Configure=0
## RUN apt-get -t testing install -y python3-setuptools -o APT::Immediate-Configure=0
## RUN apt-get -t testing install -y python3-pip -o APT::Immediate-Configure=0
## RUN apt-get -t testing install -y python3-venv -o APT::Immediate-Configure=0

## RUN pip3 install ansible
## RUN pip3 install wheel
## RUN pip3 install twine


# Añadimos el modulo de python para desplegar desde Ansible a Windows con winrm

RUN apt-get install -y libkrb5-dev
RUN apt-get install -y krb5-user


RUN pip3 install pywinrm
#RUN pip3 install pykerberos
#RUN pip3 install requests_kerberos

COPY krb5.conf /etc/

#  Add  NODEJS

RUN apt-get install -y nodejs
RUN apt-get install -y npm

# Install Docker, kubectl and helm

#RUN apt-get -qq update && \
#    apt-get -qq -y install curl && \
#    curl -sSL https://get.docker.com/ | sh && \

RUN docker --version

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl && \
    curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash


# Install Terraform

RUN wget https://releases.hashicorp.com/terraform/1.1.3/terraform_1.1.3_linux_amd64.zip && \
    unzip terraform_1.1.3_linux_amd64.zip && \
    mv terraform /usr/local/bin/ && \
    terraform --version





USER jenkins
