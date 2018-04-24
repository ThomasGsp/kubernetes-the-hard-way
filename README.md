# Kubernetes The Hard Way

This tutorial walks you through setting up Kubernetes the hard way for independent solutions 
This guide is not for people looking for a fully automated command to bring up a Kubernetes cluster. 
If that's you then check out [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine), 
or the [Getting Started Guides](http://kubernetes.io/docs/getting-started-guides/).

This project is forked from [kubernetes-the-hard-way](https://github.com/kelseyhightower/kubernetes-the-hard-way),
use some parts from [kubernetes-the-hard-way-on-azure](https://github.com/ivanfioravanti/kubernetes-the-hard-way-on-azure) 
and the official documentation [kubernetes Independent Solutions](https://kubernetes.io/docs/setup/independent/install-kubeadm/)

Kubernetes The Hard Way is optimized for learning, 
which means taking the long route to ensure you understand each task required to bootstrap a Kubernetes cluster.

> The results of this tutorial should not be viewed as production ready, 
and may receive limited support from the community, but don't let that stop you from learning!

## Target Audience

The target audience for this tutorial is someone planning to support a production Kubernetes
cluster and wants to understand how everything fits together.

## Cluster Details

Kubernetes The Hard Way guides you through bootstrapping a highly available Kubernetes cluster with
end-to-end encryption between components and RBAC authentication.

* [Kubernetes](https://github.com/kubernetes/kubernetes) 1.10.0
* [cri-containerd Container Runtime](https://github.com/kubernetes-incubator/cri-containerd) 1.0.0 
* [CNI Container Networking](https://github.com/containernetworking/cni) 0.7.0
* [etcd](https://github.com/coreos/etcd) 3.2.17

## Labs

This tutorial assumes that you have access to an physical infrastructure, 
with your own virtualization system (VMware, HyperV, Proxmox, Xen...).
With this case, we will not aboard the specifics settings for each systems...

* [Prerequisites](docs/01-prerequisites.md)  -- Adapted
* [Installing the Client Tools](docs/02-client-tools.md) -- Adapted
* [Provisioning Compute Resources](docs/03-compute-resources.md) -- Adapted
* [Provisioning the CA and Generating TLS Certificates](docs/04-certificate-authority.md) -- Work in progress
* [Generating Kubernetes Configuration Files for Authentication](docs/05-kubernetes-configuration-files.md) -- Not adapted
* [Generating the Data Encryption Config and Key](docs/06-data-encryption-keys.md) -- Not adapted
* [Bootstrapping the etcd Cluster](docs/07-bootstrapping-etcd.md) -- Not adapted
* [Bootstrapping the Kubernetes Control Plane](docs/08-bootstrapping-kubernetes-controllers.md) -- Not adapted
* [Bootstrapping the Kubernetes Worker Nodes](docs/09-bootstrapping-kubernetes-workers.md) -- Not adapted
* [Configuring kubectl for Remote Access](docs/10-configuring-kubectl.md) -- Not adapted
* [Provisioning Pod Network Routes](docs/11-pod-network-routes.md) -- Not adapted
* [Deploying the DNS Cluster Add-on](docs/12-dns-addon.md) -- Not adapted
* [Smoke Test](docs/13-smoke-test.md) -- Not adapted
* [Cleaning Up](docs/14-cleanup.md) -- Not adapted

## About the changes
I'm not a native english speaker, the documentation is probably not perfect.
I accept every language fix with pleasure :)