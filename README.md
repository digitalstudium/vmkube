# vmkube

Create virtual machines backed Kubernetes clusters on your laptop with a single command.

**One command to create clusters:** `sudo vmkube up`  
**One command to destroy clusters:** `sudo vmkube down`

## How it works

`vmkube` uses `virsh` and `talosctl` under the hood. It creates virtual machines for control plane and worker nodes, sets up isolated networking, installs Talos Linux on each VM, bootstraps Kubernetes clusters, and provides kubeconfig for immediate access. When you're done, one command removes all VMs, networks, and disks.

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

```bash
vmkube initconfig
```

it will create `~/.config/vmkube.toml` file with default configuration.
Review and modify it if necessary.

### Create clusters

```bash
sudo vmkube up
```

## Access your cluster

After creation, access Kubernetes with:

```bash
export KUBECONFIG=~/.kube/vmkube
kubectl config get-contexts
kubectl get nodes
```

### Destroy when finished

```bash
sudo vmkube down
```

## That's it
