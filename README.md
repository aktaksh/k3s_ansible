# Build a Kubernetes cluster using k3s via Ansible

The given code is taken from k3s official repo and modified to meet requirements of env.

## K3s Ansible Playbook

Build a Kubernetes cluster using Ansible with k3s. The goal is easily install a Kubernetes cluster on machines running:

- [X] Debian
- [X] Ubuntu
- [X] CentOS

on processor architecture:

- [X] x64


## System requirements

Deployment environment must have Ansible 2.4.0+
Master and nodes must have passwordless SSH access

## Usage

First create a new directory based on the `sample` directory within the `inventory` directory:

```bash
cp -R inventory/sample inventory/my-cluster
```

Second, edit `inventory/my-cluster/hosts.ini` to match the system information gathered above. For example:

```bash
[master]
192.10.10.1   --> first entry this will use as main master
193.10.10.2

[node]
192.192.10.2
192.192.10.1
192.192.10.3
192.192.10.5



[k3s_cluster:children]
master
node
```

If needed, you can also edit `inventory/my-cluster/group_vars/all.yml` to match your environment.

Start provisioning of the cluster using the following command:

```bash
ansible-playbook site.yml -i inventory/my-cluster/hosts.ini
OR if using Python3
ansible-playbook site.yml -i inventory/sample/hosts.ini -e 'ansible_python_interpreter=/usr/bin/python3'
```

## Kubeconfig

To get access to your **Kubernetes** cluster just

```bash
scp root@master_ip:~/.kube/config ~/.kube/config
```
