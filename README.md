# Kubernetes_Setup
1) Master Machine
sudo apt install docker.io
sudo systemctl enable docker
sudo apt install curl
sudo swapoff -a
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt install kubeadm
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
sudo kubectl get nodes
sudo kubectl get pods --all-namespaces

2) Worker machine
sudo apt install docker.io
sudo systemctl enable docker
sudo apt install curl
sudo swapoff -a
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt install kubeadm
--->sudo kubeadm join <command>

Kubernetes dashboard installation (master machine preferred)
1) sudo kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
2) sudo kubectl create serviceaccount dashboard-admin-sa
3)  kubectl create clusterrolebinding dashboard-admin-sa  --clusterrole=cluster-admin --serviceaccount=trackerapp:dashboard-admin-sa  (Make sure that the namespace trackerapp exists)
4)  kubectl get secrets
5)  kubectl describe secret <dashboard-admin-sa-token-dpccz>
 6) kubectl proxy (need this if running on worker machine)
Open the browser
  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/.

