# Prerequisites

## Your platform - Lab
This tutorial leverages you own physical infrastructure to streamline provisioning of the compute infrastructure required to bootstrap
a Kubernetes cluster from the ground up.
A typical Lab infrastructure can be just an standalone server (using virtualization system), different physical servers or
somethings hybrid.
In case of different physical server are using, ensure that your network is enough dimensioned to support this lab (1G link minimum).

In total, we will provide:
- 3 workers servers
- 3 masters servers
- 3 etcd servers
- 2 Load Balancer (M/S)

LB can to be a physical network appliance or two virtual machines.
Some tutorial uses the same server for masters and etcd, but to be more close from the reality, 3 independent server will be provisioned.

[--> etcd hardware](https://coreos.com/etcd/docs/latest/op-guide/hardware.html)
> * A slow disk will increase etcd request latency and potentially hurt cluster stability
> * etcd has a relatively small memory footprint but its performance still depends on having enough memory. An etcd server will aggressively cache key-value data and spends most of the rest of its memory tracking watchers. Typically 8GB is enough.
> * Few etcd deployments require a lot of CPU capacity. Typical clusters need two to four cores to run smoothly. 


### Resources

1 physical with more than 8 cpu / 24G ram or 3 smaller.  
You can setup over-allocation for CPU, it should be not a problem.  
RAM memory is the most important, in fact Workers and Masters don't use SWAP.
If you don't have enough ram memory, your process will be killed by [OOM Killer](https://www.kernel.org/doc/gorman/html/understand/understand016.html) ! 

Next: [Installing the Client Tools](02-client-tools.md)
