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
kubeadm join 192.168.50.10:6443 --token 481kqf.mhv6um6q4wspsdzr --discovery-token-ca-cert-hash sha256:44e7b5b1cda9ab75e7b08719a3e342d7c9868a90b8cd04252479a0f014e5c1fd
```

#### Setting Up kubectl on Host machine

```shell
brew install kubectl
mkdir -p $HOME/.kube
vagrant ssh master -c "sudo cat /etc/kubernetes/admin.conf" > $HOME/.kube/config.demo
export KUBECONFIG=$HOME/.kube/config.demo
source ~/.bashrc
```
