# vmkube

Create virtual machines backed Kubernetes clusters on your laptop with a single command.

**One command to create clusters:** `sudo vmkube up`  
**One command to destroy clusters:** `sudo vmkube down`

## Description

`vmkube` uses `virt-install` and `talosctl` under the hood. It creates virtual machines for control plane and worker nodes, sets up isolated networking, installs Talos Linux on each VM, bootstraps Kubernetes clusters, and provides kubeconfig for immediate access. When you're done, one command removes all VMs, networks, and disks.

It was tested on Linux, specifically debian-based distributions. It could work on other Linux distributions as well.

## Quick start

### Install dependencies

#### apt packages

```bash
sudo apt update
sudo apt install -y \
  qemu-kvm qemu-utils \
  libvirt-daemon-system libvirt-clients \
  virtinst \
  systemd-timesyncd \
  curl \
  docker.io

sudo systemctl enable --now libvirtd
```

#### talosctl

```bash
curl -sL https://talos.dev/install | sh
```

### Install vmkube

```bash
curl -OL "https://raw.githubusercontent.com/digitalstudium/vmkube/refs/heads/main/vmkube" && sudo install ./vmkube /usr/local/bin/vmkube && rm -f ./vmkube
```

### Create cconfig
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
kubectl config use-context admin@vmkube-1
kubectl get nodes
```

### Destroy when finished

```bash
sudo vmkube down
```

PRs and issues are welcomed! 
