# Playbook for Installing Basic Package


## Run Playbook

```sh
vim hosts
```

the content of **hosts**

```sh
[webservers]
192.168.1.100 ansible_ssh_port=22 ansible_ssh_user=ubuntu ansible_ssh_pass=123456789
```

Run playbook.yml

```sh
ansible-playbook -i hosts playbook.yml
```

## apt-get update 
```
- hosts: webservers
  tasks:
   - name: apt-get update
     become: true
     apt:
       upgrade: yes
       update_cache: yes
       cache_valid_time: 86400
```

## Install Package

```yml
  - name: install basic package
     become: true
     apt: pkg={{item}} state=present update_cache=yes cache_valid_time=604800
     with_items:
       - maven
       - git
       - vim
```

## Install Oracle Java

```yml
   - name: Install add-apt-repostory
     become: yes
     apt: name=software-properties-common state=latest

   - name: Add Oracle Java Repository
     become: yes
     apt_repository: repo='ppa:webupd8team/java'

   - name: Accept Java 8 License
     become: yes
     debconf: name='oracle-java8-installer' question='shared/accepted-oracle-license-v1-1' value='true' vtype='select'

   - name: Install Oracle Java 8
     become: yes
     apt: name={{item}} state=latest
     with_items:
       - oracle-java8-installer
       - ca-certificates
       - oracle-java8-set-default
```


## Official Example

[apt reference](https://docs.ansible.com/ansible/latest/modules/apt_module.html)

```yml
- name: Update repositories cache and install "foo" package
  apt:
    name: foo
    update_cache: yes

- name: Install apache httpd but avoid starting it immediately (state=present is optional)
  apt:
    name: apache2
    state: present
  environment:
    RUNLEVEL: 1

- name: Remove "foo" package
  apt:
    name: foo
    state: absent

- name: Install the package "foo"
  apt:
    name: foo

- name: Install a list of packages
  apt:
    name: "{{ packages }}"
  vars:
    packages:
    - foo
    - foo-tools

- name: Install the version '1.00' of package "foo"
  apt:
    name: foo=1.00

- name: Update the repository cache and update package "nginx" to latest version using default release squeeze-backport
  apt:
    name: nginx
    state: latest
    default_release: squeeze-backports
    update_cache: yes

- name: Install latest version of "openjdk-6-jdk" ignoring "install-recommends"
  apt:
    name: openjdk-6-jdk
    state: latest
    install_recommends: no

- name: Upgrade all packages to the latest version
  apt:
    name: "*"
    state: latest

- name: Update all packages to the latest version
  apt:
    upgrade: dist

- name: Run the equivalent of "apt-get update" as a separate step
  apt:
    update_cache: yes

- name: Only run "update_cache=yes" if the last one is more than 3600 seconds ago
  apt:
    update_cache: yes
    cache_valid_time: 3600

- name: Pass options to dpkg on run
  apt:
    upgrade: dist
    update_cache: yes
    dpkg_options: 'force-confold,force-confdef'

- name: Install a .deb package
  apt:
    deb: /tmp/mypackage.deb

- name: Install the build dependencies for package "foo"
  apt:
    pkg: foo
    state: build-dep

- name: Install a .deb package from the internet.
  apt:
    deb: https://example.com/python-ppq_0.1-1_all.deb

- name: Remove useless packages from the cache
  apt:
    autoclean: yes

- name: Remove dependencies that are no longer required
  apt:
    autoremove: yes
```

