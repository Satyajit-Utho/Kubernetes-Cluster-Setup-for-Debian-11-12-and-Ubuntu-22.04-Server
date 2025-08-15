# Kubernetes Cluster Setup for Debian 11, Debian 12 & Ubuntu 22.04 Servers

This repository contains cloud-init automation scripts to quickly set up a **multi-node Kubernetes cluster** using `kubeadm` on **Debian 11, Debian 12, and Ubuntu 22.04** servers.  
The setup includes installation of required dependencies, container runtime configuration, master node initialization, and worker node joining.

---

## Features
- **Supports** Debian 11, Debian 12, and Ubuntu 22.04.
- Installs and configures:
  - `containerd` as the container runtime with **systemd cgroup driver**
  - `kubelet`, `kubeadm`, `kubectl`
- Loads required kernel modules:
  - `overlay`
  - `br_netfilter`
- Applies necessary sysctl settings.
- Automatically initializes Kubernetes master node and generates `kubeadm join` command.
- Worker nodes automatically join the cluster using the provided join command.
- Persistent `KUBECONFIG` export for `kubectl` usage.
- Labels worker nodes for easy role identification.

---

## Prerequisites
- At least **2 servers**:
  - **Master Node**: 2 vCPU, 2 GB RAM (minimum)
  - **Worker Node(s)**: 1 vCPU, 1 GB RAM (minimum)
- All nodes should have:
  - Internet connectivity
  - Unique hostnames
  - `root` or sudo access

---

## Usage

### 1. Deploy Master Node
Run the master node **cloud-init** script during server creation or via SSH:

```bash
bash master-node.sh
