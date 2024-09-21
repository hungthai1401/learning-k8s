## Setup

### Mac Silicon

Thanks to https://github.com/techiescamp/vagrant-kubeadm-mac-silicon

### Mac Intel

```shell
mv Vagrantfile.Intel Vagrantfile
```

#### Initialize the Kubernetes Master Node

```shell
vagrant ssh master
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=192.168.50.10
...
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
sudo systemctl restart kubelet
```

#### Run in workers

```shell
sudo kubeadm join 192.168.50.10:6443 --token [TOKEN] --discovery-token-ca-cert-hash [HASH]
```

#### Setting Up kubectl on Host machine

```shell
brew install kubectl
mkdir -p $HOME/.kube
vagrant ssh master -c "sudo cat /etc/kubernetes/admin.conf" > $HOME/.kube/config.demo
export KUBECONFIG=$HOME/.kube/config.demo
source ~/.bashrc
```
