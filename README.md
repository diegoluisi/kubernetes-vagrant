# vagrant-ansible-kubernetes
Combination of Vagrant and Ansible to spin up a Kubernetes cluster

### Prerequisites
- VirtualBox
  - vagrant-vbguest
- Vagrant
- Ansible
- kubectl (optional)


### Define amount of nodes
in Vagrantfile:
```
N = 2
```


### Spin up cluster
```
$ vagrant up
```

### Verify on master
```
$ vagrant ssh k8s-master
$ kubectl get nodes
NAME         STATUS   ROLES                  AGE     VERSION
k8s-master   Ready    control-plane,master   10m     v1.21.0
node-1       Ready    <none>                 7m21s   v1.21.0
node-2       Ready    <none>                 4m37s   v1.21.0
```

### Use kubectl from local Machine
```
$ export KUBECONFIG=configs/config
```

### Verify nodes from local Machine
```
$ kubectl get nodes
NAME         STATUS   ROLES                  AGE   VERSION
k8s-master   Ready    control-plane,master   24m   v1.21.0
node-1       Ready    <none>                 19m   v1.21.0
node-2       Ready    <none>                 14m   v1.21.0
```

### Grafana
http://192.168.50.10:31000/
user: admin
pass: admin

