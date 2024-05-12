## Update the OS 
kubectl drain controlplane --ignore-daemonsets

## Update the Master OS 
apt update
apt-cache madison kubeadm



## Work on Master Node 

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.29.4-2.1 && \
apt-mark hold kubeadm

kubeadm version



kubeadm upgrade plan

 kubeadm upgrade apply v1.29.4

## kubectl uncordon <node name>
kubectl uncordon master

## Unhold and install and hold back kubelet and kubectl 

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.29.4-2.1 kubectl=1.29.4-2.1 && \
apt-mark hold kubelet kubectl

## Restart teh systemctl 

systemctl daemon-reload
systemctl restart kubelet

kubectl drain worker-02 --ignore-daemonsets


Worker Node 

apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.29.4-2.1 && \
apt-mark hold kubeadm



kubeadm upgrade node

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.29.4-2.1 kubectl=1.29.4-2.1 && \
apt-mark hold kubelet kubectl

systemctl daemon-reload
 systemctl restart kubelet
