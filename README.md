# kubeplugin — kubectl plugin for Pod Resource Metrics

This repository contains a Bash script **kubeplugin** that works as a `kubectl` plugin  
and outputs CPU and memory usage for Pods in a specified Kubernetes namespace.

The script produces output in the required CSV format:

```
Resource,Namespace,Name,CPU,Memory
```

---

## Features

- Retrieves Pod resource metrics using `kubectl top pods`
- Parses CPU and memory usage values
- Outputs clean CSV-formatted data
- Can be used as:
  - a standalone Bash script
  - a kubectl plugin (`kubectl kubeplugin`)

---

## Repository Structure

```
scripts/
└── kubeplugin
```

Ensure the script is executable:

```bash
chmod +x scripts/kubeplugin
```

---

## Requirements

- A configured Kubernetes cluster (`kubectl config current-context` must be set)
- `metrics-server` installed in the cluster
- Kubernetes v1.20+
- Bash v4+

---

## Usage (Standalone Script)

Run from the repository root:

```bash
./scripts/kubeplugin            # default namespace
./scripts/kubeplugin kube-system
```

### Example Output (real cluster: kube-system)

```
Resource,Namespace,Name,CPU,Memory
pod,kube-system,coredns-66bc5c9577-649nl,6m,68Mi
pod,kube-system,etcd-minikube,27m,58Mi
pod,kube-system,kube-apiserver-minikube,59m,272Mi
pod,kube-system,kube-controller-manager-minikube,26m,105Mi
pod,kube-system,kube-proxy-xw99m,3m,54Mi
pod,kube-system,kube-scheduler-minikube,13m,63Mi
pod,kube-system,metrics-server-85b7d694d7-6qlrl,7m,17Mi
pod,kube-system,storage-provisioner,5m,10Mi
```

---

## Usage (kubectl Plugin)

1. Create a symlink inside a directory included in your `$PATH`:

```bash
ln -s "$(pwd)/scripts/kubeplugin" "$HOME/.local/bin/kubectl-kubeplugin"
```

2. Run the plugin:

```bash
kubectl kubeplugin
kubectl kubeplugin kube-system
```

---

## Help

```bash
kubectl kubeplugin --help
```

---
