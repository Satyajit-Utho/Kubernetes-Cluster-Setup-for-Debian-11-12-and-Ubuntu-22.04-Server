# Kubernetes Cluster Setup for Debian 11, Debian 12, and Ubuntu 22.04

This guide will help you quickly set up a Kubernetes cluster using kubeadm on Debian 11, Debian 12, or Ubuntu 22.04 servers.

---

## 1. Master Node Setup

Run this script on your **Master Node**:

```bash
curl -fsSL https://raw.githubusercontent.com/<your-github-username>/<your-repo>/main/master-node.sh | bash
After setup completes, your join command will be shown automatically.

You can also get the join command anytime by running:

bash
Copy
Edit
kubeadm token create --print-join-command
2. Worker Node Setup
Run this script on each Worker Node:

bash
Copy
Edit
curl -fsSL https://raw.githubusercontent.com/<your-github-username>/<your-repo>/main/worker-node.sh | bash
3. Verify Cluster Status
On the Master Node, check all nodes:

bash
Copy
Edit
kubectl get nodes -o wide
Check all system pods:

bash
Copy
Edit
kubectl get pods -n kube-system -o wide
4. Assign Worker Role Label
If your worker node is not automatically labeled, run:

bash
Copy
Edit
kubectl label node <worker-node-name> node-role.kubernetes.io/worker=worker
Example:

bash
Copy
Edit
kubectl label node workernode1 node-role.kubernetes.io/worker=worker
5. Troubleshooting
Node shows NotReady:
Check CNI plugin:

bash
Copy
Edit
kubectl get pods -n kube-flannel
Reinstall Flannel if needed:

bash
Copy
Edit
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
Join Command Expired:
Generate a new one:

bash
Copy
Edit
kubeadm token create --print-join-command
