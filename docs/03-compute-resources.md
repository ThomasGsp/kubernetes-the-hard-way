# Provisioning Compute Resources

Kubernetes requires a set of machines to host the Kubernetes control plane and the worker nodes where containers are ultimately run. 
In this lab you will provision the compute resources required for running a secure and highly available Kubernetes cluster.


## Networking / Physical view

The Kubernetes [networking model](https://kubernetes.io/docs/concepts/cluster-administration/networking/#kubernetes-model) assumes a flat network in which containers and nodes can communicate with each other. In cases where this is not desired [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) can limit how groups of containers are allowed to communicate with each other and external network endpoints.

Example with 3 physical servers (very basic architecture, do not use same in production!):  
![physical view](https://github.com/ThomasGsp/kubernetes-the-hard-way_Independent-Solutions/blob/master/img/physical_view.png)

> Setting up network policies is out of scope for this tutorial.


###  IP Address allocation

Static IP
> - Worker 0: 172.16.5.100/24
> - Worker 1: 172.16.5.101/24
> - Worker 2: 172.16.5.102/24

> - Master 0: 172.16.5.10/24
> - Master 1: 172.16.5.11/24
> - Master 2: 172.16.5.12/24

> - Etcd 0: 172.16.5.20/24
> - Etcd 1: 172.16.5.21/24
> - Etcd 2: 172.16.5.22/24
 
> - LB 0: 172.16.5.30/24
> - LB 1: 172.16.5.31/24

Allocate a static IP address that will be attached to the external load balancer fronting the Kubernetes API Servers.
> - Vip: 172.16.5.200/24

Others attributions:
> - GW: 172.16.5.254/24
> - HYP1:  172.16.5.1/24
> - HYP2:  172.16.5.2/24 (If exist)
> - HYP3:  172.16.5.3/24 (If exist)

You can choose an other network, my network 172.16.0.0/24 was already used.  
Use 172.16.5.100 to 172.16.5.199 allow the possibility to extend the number of worker in keeping an logical network.  
But probably that you'll not setup 100 workers !

Each worker instance requires a pod subnet allocation from the Kubernetes cluster CIDR range.
The pod subnet allocation will be used to configure container networking in a later exercise. 
The `pod-cidr` instance metadata will be used to expose pod subnet allocations to compute instances at runtime.

> The Kubernetes cluster CIDR range is defined by the Controller Manager's `--cluster-cidr` flag. In this tutorial the cluster CIDR range will be set to `10.200.0.0/16`, which supports 254 subnets.


## Compute Instances
The compute instances in this lab will be provisioned using [Debian](https://www.debian.org) stretch, 
which has good support for the [cri-containerd container runtime](https://github.com/containerd/cri-containerd). 
Each compute instance will be provisioned with a fixed private IP address to simplify the Kubernetes bootstrapping process.

### Instances - Controllers ( == Master )
Create three compute instances which will host the Kubernetes control plane:

Minimum:
- 1 CPU
- 2G RAM
- 10G Disk

- Debian 9 fresh install (or ubuntu)
- No swap

### Instances - Etcd

Create three compute instances which will host etcd database:

Minimum:
- 1 CPU
- 1G RAM
- 10G Disk

- Debian 9 fresh install (or ubuntu)


### Instances - Workers

Create three compute instances which will host the Kubernetes worker nodes:

Minimum:
- 2 CPU
- 4G RAM
- 50G Disk

- Debian 9 fresh install (or ubuntu)
- No swap 



Next: [Provisioning a CA and Generating TLS Certificates](04-certificate-authority.md)
