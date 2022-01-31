# kubernetes-vagrant
Combination of Vagrant and Ansible to spin up a multi node Kubernetes cluster

### Objective 
This blog post describes the steps required to setup a multi node Kubernetes cluster for development purposes. This setup provides a production-like cluster that can be setup on your local machine.

### Why do we require multi node cluster setup? 
Multi node Kubernetes clusters offer a production-like environment which has various advantages. Even though Minikube provides an excellent platform for getting started, it doesn't provide the opportunity to work with multi node clusters which can help solve problems or bugs that are related to application design and architecture. For instance, Ops can reproduce an issue in a multi node cluster environment, Testers can deploy multiple versions of an application for executing test cases and verifying changes. These benefits enable teams to resolve issues faster which make the more agile.

### Why use Vagrant and Ansible?
Vagrant is a tool that will allow us to create a virtual environment easily and it eliminates pitfalls that cause the works-on-my-machine phenomenon. It can be used with multiple providers such as Oracle VirtualBox, VMware, Docker, and so on. It allows us to create a disposable environment by making use of configuration files.

Ansible is an infrastructure automation engine that automates software configuration management. It is agentless and allows us to use SSH keys for connecting to remote machines. Ansible playbooks are written in yaml and offer inventory management in simple text files.



### Prerequisites
- Git - [How to](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- VirtualBox - [How to](https://www.virtualbox.org/wiki/Linux_Downloads)
  - vagrant-vbguest
- Vagrant [How to](https://www.vagrantup.com/downloads)
- Ansible [How to](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- kubectl (optional) [How to](https://github.com/ahmetb/kubectx#installation)

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

### Customize
```code
$ vim kubernetes-setup/master-playbook.yml
```

### Grafana
```markdown
http://192.168.50.10:31000/   
user: admin   
pass: admin
````

### Debugging
```code
$ vagrant up 

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
### Destroy de env
````code
$ vagrant destroy
````
