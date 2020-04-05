# Kubernetes_Setup
1) Master Machine
  a) sudo apt install docker.io
  b) sudo systemctl enable docker
  c) sudo apt install curl
  d) sudo swapoff -a
  e) sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
  f) sudo apt install kubeadm
  g) sudo kubeadm init --pod-network-cidr=10.244.0.0/16
  h) mkdir -p $HOME/.kube
  i) sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  j) sudo chown $(id -u):$(id -g) $HOME/.kube/config
  k) sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
  l) sudo kubectl get nodes
  m) sudo kubectl get pods --all-namespaces

2) Worker machine
  a) sudo apt install docker.io
  b) sudo systemctl enable docker
  c) sudo apt install curl
  d) sudo swapoff -a
  e) sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
  f) sudo apt install kubeadm
  g) --->sudo kubeadm join <command>

Kubernetes dashboard installation (master machine preferred)
1) sudo kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
2) sudo kubectl create serviceaccount dashboard-admin-sa
3)  --> kubectl create clusterrolebinding dashboard-admin-sa  --clusterrole=cluster-admin --serviceaccount=trackerapp:dashboard-admin-sa  (Make sure that the namespace trackerapp exists)
4)  kubectl get secrets
5)  --> kubectl describe secret <dashboard-admin-sa-token-dpccz>
 6) kubectl proxy (need this if running on worker machine)
Open the browser
  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.

