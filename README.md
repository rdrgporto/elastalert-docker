# Welcome to Elastalert Docker! :whale: :sailboat:

This repository was created in order to make easier to integrate **Elastalert** on **Docker**.

## First Steps

* Download **Docker** : [Link](https://docs.docker.com/install/linux/docker-ce/ubuntu/#os-requirements)
* **Elastalert** doc: [Link](https://elastalert.readthedocs.io/en/latest/)

## Create/Edit Dockerfile

If you want to edit the image, for example, change to a new version, install a new package, and so on, you can follow this guide:

Download **repository**:

```
git clone https://github.com/rdrgporto/elastalert-docker.git
```

Edit **Dockerfile** with your favorite text editor and create image:

```
docker build -t john-doe/elastalert-docker
```

Run **container**:

```
docker run --name elastalert-docker-test john-doe/elastalert-docker
```
