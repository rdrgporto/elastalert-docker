# Welcome to Elastalert Docker! :whale:

This repository was created in order to make easier to integrate **Elastalert** on **Docker**.

## First Steps

* Install **Docker** : [Link](https://docs.docker.com/engine/install/)
* Take a quick look over **Elastalert** doc: [Link](https://elastalert.readthedocs.io/en/latest/)

## Up

If you want to edit the image, for example, change to a new version, install a new package, and so on, you can follow this guide:

### <u>Install Git</u>

- #### Linux :penguin:

```bash
sudo apt -y install git --> Ubuntu/Debian
sudo yum -y install git --> CentOS/RedHat

git clone https://github.com/rdrgporto/elastalert-docker.git
```

- #### Windows :checkered_flag:

  Download [Git Bash](https://gitforwindows.org/) and install it:

```bash
git clone https://github.com/rdrgporto/elastalert-docker.git
```

### <u>Run</u> :rocket:

Create **Docker** image:

```bash
docker image build -t elastalert-docker:latest -f Dockerfile .
```

Run container:

```bash
docker container run --name elastalert elastalert-docker:latest 
```
