---
layout: post
published: true
title: Ansible Playbook for ELK Server 5.4 with Machine Learning
---

# ELK - Server

## Intro

This is an ansible playbook to provision a single ELK Server (All-in-one). It implement many rol as ntp, firewalld, curator, beats, beats-win (windows beats) and it has proxy and selinux features enabled (by default)

## Requirements


* Ansible 2.1
* CentOS 7.x (minimal version)


## Installation


### Step 1: Define your global vars in groups/all/main.yml

Example, to install the last ELK version, with beta machine learning module:

```
elk_version: 5.4.0
```

### Step 2: Add the ip or hostname in inventory-prd file

```
[elk]
10.253.253.101
```

### Step 3: Run the playbook and enjoy

```sh
git clone https://github.com/jenciso/elk-server
cd elk-server
sudo ansible-playbook site.yml -i inventory
```


## Example

### Running the playbook

[![asciicast](https://asciinema.org/a/9kpvd5rqy96dv4og1ctzh71vy.png)](https://asciinema.org/a/9kpvd5rqy96dv4og1ctzh71vy)

### Monitor

![Monitor](/img/elk01.png?raw=true "Monitor")

### Machine Learning

![Machine Learning](/img/elk02.png?raw=true "Machine Learning")

### Logs

![Logs](/img/elk03.png?raw=true "Logs")

## Author
Juan Enciso

juan.enciso@gmail.com
