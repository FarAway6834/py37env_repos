# Project

### Subrepo Struct and File Values
#### REPO & files
##### [py37env_home <REPO>](https://github.com/FarAway6834/py37env_home)
 - py37env_runbash
 - activate
 - initial_setting
 - initial_setter
 - ... etc

##### [py37env_dockerdeploy_workspace <REPO>](https://github.com/FarAway6834/py37env_dockerdeploy_workspace)
 - Dockerfile
 - ... etc

#### File Source Values!

py37env_runbash
```
#!/bin/bash

. ./activate
echo "default passwd is passwd, username is py37 mean python3.7 env usr"
exec bash -i
```

activate
```
#!/bin/bash

. ./.venv/bin/activate
```

initial_setting
```
#!/bin/bash

sudo apt-get install software-properties-common -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update -y
sudo apt-get install python3.7

python3.7 -m venv .venv

chmod u+x ./py37env_runbash
chown -R py37:py37 /home/py37

rm initial_setter
rm initial_setting
rm umm.md
```

initial_setter (deployment by github page)
```
#!/bin/bash

useradd -m -s /bin/bash py37
echo "py37:passwd" | chpasswd
adduser py37 sudo

git clone https://github.com/FarAway6834/py37env_home /home/py37/py37env_home
/home/py37/py37env_home/initial_setting
rm ./initial_setter
```

Dockerfile
```
FROM ubuntu:20.04

RUN apt-get -y update -y && \
    apt-get -y upgrade -y && \
    apt-get install git -y && \
    apt-get install wget -y && \
    wget https://faraway6834.github.io/py37env_home/initial_setter && \
    ./initial_setter

WORKDIR /home/py37/py37env_home

USER py37

CMD ["bash", "./py37env_runbash"]
```
