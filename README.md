# vagrant-kubernetes
Combination of Vagrant and Ansible to spin up a Kubernetes cluster

### Prerequisites
- Git - [How to Install](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- VirtualBox - [Download and Install](https://www.virtualbox.org/wiki/Linux_Downloads)
  - vagrant-vbguest
- Vagrant [How to Install](https://www.vagrantup.com/downloads)
- Ansible [How to Install](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- kubectl (optional) [How to Install](https://github.com/ahmetb/kubectx#installation)

### Clone the repository
```code
git clone git@github.com:diegoluisi/vagrant-kubernetes.git
cd vagrant-kubernetes
```

### Define amount of nodes
in Vagrantfile:
```code
N = 2
```
### Instal vagrant-vbguest plugin
```code
$ vagrant plugin install vagrant-vbguest  
```

### Spin up cluster
```code
$ vagrant up
```

### Verify on master
```code
$ vagrant ssh k8s-master
$ kubectl get nodes
NAME         STATUS   ROLES                  AGE     VERSION
k8s-master   Ready    control-plane,master   10m     v1.21.0
node-1       Ready    <none>                 7m21s   v1.21.0
node-2       Ready    <none>                 4m37s   v1.21.0
```

### Use kubectl from local Machine
```code
$ export KUBECONFIG=configs/config
```

### Verify nodes from local Machine
```code
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

### Debugging
```code
 vagrant up 

Bringing machine 'k8s-master' up with 'virtualbox' provider...
Bringing machine 'node-1' up with 'virtualbox' provider...
==> k8s-master: Checking if box 'bento/ubuntu-18.04' version '202112.19.0' is up to date...
==> k8s-master: Clearing any previously set network interfaces...
The IP address configured for the host-only network is not within the
allowed ranges. Please update the address used to be within the allowed
ranges and run the command again.

  Address: 192.168.50.10
  Ranges: 

Valid ranges can be modified in the /etc/vbox/networks.conf file. For
more information including valid format see:

  https://www.virtualbox.org/manual/ch06.html#network_hostonly
```
###
``` code
# sudo vim /etc/vbox/networks.conf
* 0.0.0.0/0 ::/0
```