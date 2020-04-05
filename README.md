# Kubernetes_Setup

1) Master Machine
  a) sudo swapoff -a
  b) sudo apt install docker.io
  c) sudo systemctl enable docker
  d) sudo apt install curl
  e) curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
  f) sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
  g) sudo apt install kubeadm
  h) sudo kubeadm init --pod-network-cidr=10.244.0.0/16
  i) mkdir -p $HOME/.kube
  j) sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  k) sudo chown $(id -u):$(id -g) $HOME/.kube/config
  l) sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
  m) sudo kubectl get nodes
  n) sudo kubectl get pods --all-namespaces

2) Worker machine
  a) sudo swapoff -a
  b) sudo apt install docker.io
  c) sudo systemctl enable docker
  d) sudo apt install curl
  e) curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
  f) sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
  g) sudo apt install kubeadm
  h) --->sudo kubeadm join <command>

Kubernetes dashboard installation (master machine preferred)
1) sudo kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
2) sudo kubectl create serviceaccount dashboard-admin-sa
3)  --> kubectl create clusterrolebinding dashboard-admin-sa  --clusterrole=cluster-admin --serviceaccount=trackerapp:dashboard-admin-sa  (Make sure that the namespace trackerapp exists)
4)  kubectl get secrets
5)  --> kubectl describe secret <dashboard-admin-sa-token-dpccz>
6) kubectl proxy
Open the browser
  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.

