# Playbook for Running Docker

## Install Docker

playbook-docker.yml

```yml
- hosts: webservers
  become: true
  tasks:
  - name: Add Docker GPG key
    apt_key: url=https://download.docker.com/linux/ubuntu/gpg

  - name: Add Docker APT repository
    apt_repository:
      repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ansible_distribution_release}} stable

  - name: Install list of packages
    apt:
      name: "{{ item }}"
      state: present
      update_cache: yes
    with_items:
      - apt-transport-https
      - ca-certificates
      - curl
      - software-properties-common
      - docker-ce
```

## Set up Module for Docker

1. install easy_install
2. install pip
3. install docker-py


```yml
  - name: Easy Install
    apt:
      name: python-setuptools
      state: present

  - name: Install pip
    easy_install:
     name: pip
     state: latest

  - name: pip install docker-py
    pip:
      name: docker-py
```

## Docker Pull

Using **docker_image** module

```yml
  - name: Docker Pull Image
    docker_image:
      name: library/mysql
      tag: 5.6
```

## Docker Run

Using **docker_container** module

```yml
  - name: Run Docker
    docker_container:
      name: mysql56
      image: library/mysql
      state: started
      restart: yes
      ports:
        - "3306:3306"
      env:
        MYSQL_ROOT_PASSWORD: lucas1234
        MYSQL_DATABASE: mydb
        MYSQL_USER: lucas
        MYSQL_PASSWORD: lucas1234
      volumes:
        - /data:/var/lib/mysql
```

## Reference of Module

1. [docker_image](https://docs.ansible.com/ansible/2.6/modules/docker_image_module.html)

2. [docker_container](https://docs.ansible.com/ansible/2.5/modules/docker_container_module.html)



