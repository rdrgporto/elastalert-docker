# Welcome to Elastalert Docker! :whale: :sailboat:

This repository was created in order to make easier to integrate **Elastalert** on **Docker**. Moreover, it is possible to integrate it on **Kubernetes**.

## First Steps

 - Download **Docker** : [Link](https://docs.docker.com/install/linux/docker-ce/ubuntu/#os-requirements)
 - Download **Kubernetes**: [Link](https://kubernetes-v1-4.github.io/)

## Deployment on Docker

First of all, it is necessary to create config and rules directory. Inside these directories, you have to copy/create config files. An example:

    /home/rdrgporto/elastalert# tree
    .
    ├── config
    │   ├── elastalert_config.yaml
    │   └── elastalert_supervisord.conf
    └── rules
        └── example-rule.yaml
    2 directories, 3 files

    docker run -d \
        -v `pwd`/config/:/opt/elastalert/config/ \
        -v `pwd`/rules:/opt/elastalert/rules \
        --name elastalert-docker rdrg/elastalert-docker

By default, the timezone is **Europe/Madrid**, if you want to change it:

    docker run -d -e "TZ=Europe/Paris" \
        -v `pwd`/config/:/opt/elastalert/config/ \
        -v `pwd`/rules:/opt/elastalert/rules \
        --name elastalert-docker rdrg/elastalert-docker

## Create/Edit Dockerfile

If you want to edit the image, for example, change to a new version, install a new package, and so on, you can follow this guide:

Download **repository**:

    git clone https://github.com/rdrgporto/elastalert-docker.git

Edit **Dockerfile** with your favorite text editor and create image:

    docker build -t john-doe/elastalert-docker

Run **container**:

    docker run --name elastalert-docker-test john-doe/elastalert-docker

## Deployment on Kubernetes

Download **repository**:

    git clone git clone https://github.com/rdrgporto/elastalert-docker.git

Deploy **Elastalert** pod:

    cd elastalert-docker
    kubectl create -f kubernetes/
