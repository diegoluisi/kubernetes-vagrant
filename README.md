#1) Baixa as chaves GPG da oracle:
$ wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
$ wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

2)Adiciona o repositório do virtualbox:
$ sudo add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib"

3)Instala o VirtualBox:
$ sudo apt update
$ sudo apt install virtualbox-6.0

4)Instala headers do kernel e umas bibliotecas necessárias para  compilação:
$ sudo apt-get install build-essential linux-headers-$(uname -r) dkms virtualbox-dkms

5) Ativa o modulo do kernel:
$ sudo modprobe vboxdrv
