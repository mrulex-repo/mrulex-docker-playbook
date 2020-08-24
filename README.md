# Playbook to install and setup Docker and a Docker Swarm cluster

This playbook can be used to install Docker and also to setup Docker Swarm cluster.

## What does it do?

* Install Docker
* Creates Swarm Cluster, based on inventory
* Add Docker Managers into Swarm Cluster, based on inventory
* Add Docker Workers into Swarm Cluster, based on inventory
* ~~Configure nodes in Swarm Cluster~~
* ~~Remove non defined nodes from Swarm Cluster~~

## Hosts in inventory are:

* **docker_instances** for all instances to install Docker. Whether it belongs to the cluster or not.
* **docker_managers** all manager instances in cluster, this group must be child of *docker_instances*
* **docker_workers** all worker instances in cluster, this group must be child of *docker_instances*

## Variables:

* **docker_version** for all hosts, version to install
* **docker_advertise_address** per host, this is used to define the advertise address for the docker host into the Swarm cluster. If not defined it uses *ansible_default_ipv4.address* host variable.
* **docker_node_labels** labels to be assigned to docker instances

## Usage:
```
ansible-playbook -i <inventory> setup.yml
```

## Samples:

### Inventory to install Docker
*File: hosts*
```
[docker_instances]
docker1
docker2
docker3
```

### Inventory to install Docker and setup cluster
*File: hosts*
```
[docker_managers]
manager1
manager2
manager3

[docker_workers]
worker1
worker2
worker3

[docker_instances:children]
docker_managers
docker_workers
```
