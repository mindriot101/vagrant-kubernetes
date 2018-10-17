# Kubernetes on bare metal installation process

## Notes

- Primarily following: [Creating a single master cluster with kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
- Started with Raspberry Pi
- Moved on to example VMs
- Trying to use CentOS 7
- Works with flannel networking but using the latest commit

## Commands

- `vagrant up`
- `ansible playbook -i hosts site.yml`
- Ensure all hosts are routable via /etc/hosts (VM specific)
- Install docker using [Docker CE instructions](https://docs.docker.com/install/)
- Install k8s via [kubeadm documentation](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/)
- Use the following options to `kubeadm init`:
    - `--apiserver-advertise-address 192.168.33.10` - IP address of the master node in the private network
    - `--pod-network-cidr 10.244.0.0/16` - for Flannel
- Chose flannel for pod network with [current master setup yaml file](https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml)
- nginx-ingress [install](https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml) then [expose node port service](https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/baremetal/service-nodeport.yaml)
- metallb ([install](https://raw.githubusercontent.com/google/metallb/v0.7.3/manifests/metallb.yaml) then expose with [default config](https://raw.githubusercontent.com/google/metallb/v0.7.3/manifests/example-layer2-config.yaml))
