# vmkube

Create and destroy virtual machines backed Kubernetes clusters on your laptop with a single command.

**One command to create clusters:** `sudo vmkube up`  
**One command to destroy clusters:** `sudo vmkube down`

## How it works

vmkube creates Kubernetes clusters using KVM virtual machines. It handles everything automatically:

1. Creates virtual machines for control plane and worker nodes
2. Sets up isolated networking
3. Installs Talos Linux on each VM
4. Bootstraps a production-ready Kubernetes cluster
5. Provides kubeconfig for immediate access

When you're done, one command removes all VMs, networks, and disks.

## Quick start

### Install requirements

```bash
sudo apt install -y qemu-kvm libvirt-daemon-system virt-manager systemd-timesyncd
sudo usermod -a -G libvirt $USER
newgrp libvirt
```

### Install vmkube

```bash
sudo apt install -y vmkube
```

### Create config

pick `vmkube.toml` from this repository, modify it if necessary and place it here: `~/.config/vmkube.toml`

### Create your first cluster

```bash
sudo vmkube up
```

## Access your cluster

After creation, access Kubernetes with:

```bash
kubectl config get-contexts
kubectl use-context admin@vmkube-1
kubectl get nodes
```

### Destroy when finished

```bash
sudo vmkube down
```

## That's it
