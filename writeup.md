# Kubernetes on bare metal installation process

## Notes

- Primarily following: [Creating a single master cluster with kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
- Started with Raspberry Pi
- Moved on to example VMs
- Trying to use CentOS 7
- Works with flannel networking but using the latest commit

## Commands

- Ensure all hosts are routable via /etc/hosts (VM specific)
- Install docker using [Docker CE instructions](https://docs.docker.com/install/)
- Install k8s via [kubeadm documentation](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
- Use the following options to `kubeadm init`:
    - `--apiserver-advertise-address 192.168.33.10` - IP address of the master node in the private network
    - `--pid-network-cidr 10.244.0.0/16` - for Flannel
- Chose flannel for pod network with [current master setup yaml file](https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml)
