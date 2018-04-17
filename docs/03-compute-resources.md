# Provisioning Compute Resources

Kubernetes requires a set of machines to host the Kubernetes control plane and the worker nodes where containers are ultimately run. 
In this lab you will provision the compute resources required for running a secure and highly available Kubernetes cluster.


## Networking / Physical view

The Kubernetes [networking model](https://kubernetes.io/docs/concepts/cluster-administration/networking/#kubernetes-model) assumes a flat network in which containers and nodes can communicate with each other. In cases where this is not desired [network policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/) can limit how groups of containers are allowed to communicate with each other and external network endpoints.

Example with 3 physical servers:
![physical view](/img/physical_view.png  =600x400)

> Setting up network policies is out of scope for this tutorial.


###  IP Address allocation
Allocate a static IP address that will be attached to the external load balancer fronting the Kubernetes API Servers.

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

> - Vip: 172.16.5.200/24

Others attributions:
> - GW: 172.16.5.254/24
> - HYP1:  172.16.5.1/24
> - HYP2:  172.16.5.2/24 (If exist)
> - HYP3:  172.16.5.3/24 (If exist)

You can choose an other network, my network 172.16.0.0/24 was already used.  
Use 172.16.5.100 to 172.16.5.199 allow the possibility to extend the number of worker in keeping an logical network.  
But probably that you'll not setup 100 workers !

## Compute Instances
The compute instances in this lab will be provisioned using [Debian](https://www.debian.org) stretch, 
which has good support for the [cri-containerd container runtime](https://github.com/containerd/cri-containerd). 
Each compute instance will be provisioned with a fixed private IP address to simplify the Kubernetes bootstrapping process.

### Kubernetes Controllers ( == Master )

Create three compute instances which will host the Kubernetes control plane:



### Kubernetes Workers

Each worker instance requires a pod subnet allocation from the Kubernetes cluster CIDR range. The pod subnet allocation will be used to configure container networking in a later exercise. The `pod-cidr` instance metadata will be used to expose pod subnet allocations to compute instances at runtime.

> The Kubernetes cluster CIDR range is defined by the Controller Manager's `--cluster-cidr` flag. In this tutorial the cluster CIDR range will be set to `10.200.0.0/16`, which supports 254 subnets.

Create three compute instances which will host the Kubernetes worker nodes:

```
for i in 0 1 2; do
  gcloud compute instances create worker-${i} \
    --async \
    --boot-disk-size 200GB \
    --can-ip-forward \
    --image-family ubuntu-1604-lts \
    --image-project ubuntu-os-cloud \
    --machine-type n1-standard-1 \
    --metadata pod-cidr=10.200.${i}.0/24 \
    --private-network-ip 10.240.0.2${i} \
    --scopes compute-rw,storage-ro,service-management,service-control,logging-write,monitoring \
    --subnet kubernetes \
    --tags kubernetes-the-hard-way,worker
done
```

### Verification

List the compute instances in your default compute zone:

```
gcloud compute instances list
```

> output

```
NAME          ZONE        MACHINE_TYPE   PREEMPTIBLE  INTERNAL_IP  EXTERNAL_IP     STATUS
controller-0  us-west1-c  n1-standard-1               10.240.0.10  XX.XXX.XXX.XXX  RUNNING
controller-1  us-west1-c  n1-standard-1               10.240.0.11  XX.XXX.X.XX     RUNNING
controller-2  us-west1-c  n1-standard-1               10.240.0.12  XX.XXX.XXX.XX   RUNNING
worker-0      us-west1-c  n1-standard-1               10.240.0.20  XXX.XXX.XXX.XX  RUNNING
worker-1      us-west1-c  n1-standard-1               10.240.0.21  XX.XXX.XX.XXX   RUNNING
worker-2      us-west1-c  n1-standard-1               10.240.0.22  XXX.XXX.XX.XX   RUNNING
```

Next: [Provisioning a CA and Generating TLS Certificates](04-certificate-authority.md)
