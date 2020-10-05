# Kubeadm Cluster Ansible Role

This Ansible role will setup a [Kuberenetes](https://github.com/kubernetes/kubernetes)
cluster using [Kubeadm](https://github.com/kubernetes/kubeadm). Goals of this
role include being both idempotent as well as supporting upgrading existing
clusters when necessary. Additionally, a goal is to provide some flexibility
with CNI and other settings, however, currently this isn't implemented.

In its current state, this role is incomplete and opinionated. This includes
only targeting small clusters with a distributed control plane nodes, and the
use of the Calico CNI plugin. In the future, support could be added to have
separate control-plane and worker nodes

This role has only been tested with Debian and would need tasks to install
required software on RedHat, CentOS, and others.

## Requirements

This role has only been tested with Debian, but should support Ubuntu. Support
for RHEL and CentOS has not yet been added.

* Ansible - 2.9+ recommended

## Variables

The following variables are supported. When using this role, set variables
inside the role context. For example:

```yaml
  roles:
  - name: kubeadm
    vars:
      kube_version: "1.18.1"
```

### `kube_version`

- Set the version of Kubeadm and Kubernetes to use
  - This field does not use the 'v' prefix before the version
- Default: *1.18.1*

### `kube_cgroup_driver`

- Specify which control group driver to use
  - Possible values: `cgroupfs`, `systemd`
  - Not currently tested with `cgroupfs`
- Default: *systemd*

### `kube_container_runtime`

- Specify which container runtime to use
  - Possible values: `containerd`
- Default: *containerd*

### `kube_custom_cni`

- Enable support for customizing CNI plugin use in the cluster, including using the CNI DHCP server
  - This is in addition to the default CNI network plugin deployed such as Calico or Flannel
- Supports the [standard CNI plugins](https://github.com/containernetworking/plugins) which are always included with Kubeadm
- Default: *no*

### `kube_systemd_directory`

- Base folder for systemd configuration
- Default: */etc/systemd/system*
