# Kubernetes The Hardware Way

This tutorial walks you through setting up Kubernetes on bare metal machines (no virtualization) with [Talos Linux](https://talos.dev)
This guide is not for someone looking to run Kubernetes in a virtualized environment like AWS.
It is intended for people who want to create a home lab with spare computers, companies that run hardware in data centers, or people running hardware in constrained environments like edge.

This tutorial is optimized for learning how you can install Talos Linux and deploy Kubernetes with it.

> The results of this tutorial should not be viewed as production ready, and may receive limited support from the community, but don't let that stop you from learning!

## Copyright

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.

## Target Audience

The target audience for this tutorial is someone who wants to understand how to go from a brand new computer to a Kubernetes API.
You may have limited experience with Linux and Kubernetes and aren't interested in doing everything manually.

## Cluster Details

Kubernetes The Hardware Way guides you through bootstrapping a basic Kubernetes cluster with all control plane components running on a single node, and one worker node.
You should have 2 computers to complete this tutorial.

There are alternative configuration instructions if you only have a single computer.

> There is some support for single board computers with Talos Linux but it is not recommended because of their limited resources (CPU and memory) and the extra complexity to install Linux to them.

The ideal computers will have these minimum specs:

- CPU with amd64/x86_64 architecture
- minimum of 8GB of memory
- minimum of 40GB hard drive (ssd preferred)

The machines should be reachable on the same network as your computer and all computers will need internet access.
You will also need a USB drive to boot the machines from to install Talos.

Component versions:

- [Talos Linux](https://talos.dev) v1.7.x
- [Kubernetes](https://github.com/kubernetes/kubernetes) v1.30.x

All of the other components (e.g. etcd, containerd) will be installed automatically and you shouldn't care about which versions are used.

## Labs

The lab will

- [Prerequisites](docs/01-prerequisites.md)
- [Download Talos Linux](docs/02-download.md)
- [Boot Talos Linux](docs/03-boot.md)
- [Generate configuration](docs/04-config.md)
- [Apply config](docs/05-apply-config.md)
- [Use Kubernetes](docs/06-kubernetes.md)
- [Cleaning Up](docs/99-cleanup.md)
