---
layout: post
title: Use Docker for Ansible playbook work out
comments: true
created: 1481797574
excerpt_separator: <!--more-->
---

Sigfox Infrastructure team deploy most of things with Ansible.

In our way to full DevOps, we delegate Ansible deployment playbook creation to software development teams.

But:
* we don't have enough development VM or "on demand" VM to tune our scripts
* we are humans and make a lot of iterations before having a working playbook

That is why we use Docker.

<!--more-->

Docker image versionning can be done in two ways:
* using "docker commit" and a docker repository (public or private)
* using DockerFiles and git

The second one is my favorite because git is a _loooot_ more powerfull and reliable than docker versionning.
Using sinmple text files matches more with Unix philosophy and _culture of low_ we have at Sigfox (Marketing say _Power of Low_).

# DockerFile repository

We put all our DockerFile in a git repository.

Some images for development purpose, some other one are copies of production configuration.

To illustrate this, suppose that we have ubuntu server 14.04 in production.

This is Docker image I will use :

```
FROM ubuntu:14.04
MAINTAINER Xavier Raffin <xavier.raffin@sigfox.com>

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:secretpassword' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
```

This docker file is based on ubuntu 14.04 official image and add ssh access for root with password _"secretpassword"_.


## How to use DockerFile

First build docker image.
Here I name it "mapserver"

```
docker build -t mapserver /path/of/your/dockerfile/dir
```

Then create a container (I call it 'map1') and launch it:

```
docker run -d --name map1 mapserver
```

Or with a data directory and port forwarding:

```
docker run -d -v /host/directory/to/map/:/container/mountpoint -p80:80  --name map1 mapserver
```

Then, you need to get container IP address:

```
docker inspect map1 | grep IPAddress
```

Then connect (login/pass = root/secretpassword) to check access

```
ssh root@172.17.0.2 
```

If something goes wrong and you need a terminal on the container do:

```
docker exec -it map1 bash
```

Then if you want ssh keys instead of password do:

```
cat ~/.ssh/id_rsa.pub | ssh root@172.17.0.2 "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```

Then you have a good base to play with Ansible

# Ansible

Now you have a container similar to production servers and you can tune youre Ansible playbooks.

Just basic reminder : you need to add container in your ansible host list
In /etc/ansible/hosts you will have something like this : 

```
[docker]
172.17.0.2 server_name=map1
```

Then check connection 
```
ansible all -m ping -u root
```

When done you can start working with your playbook
```
ansible-playbook -u root deploy.yml
```





