Thanks to 

OpenStack Support in Kubernetes group.

This document is donated by them.


In command line:
	
	sudo passwd

	setenforce 0
	sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
reboot


Master configuration:

 Install firewalld: 

	yum install firewalld -y
	systemctl start firewalld && systemctl enable firewalld
	firewall-cmd --permanent --add-port=6443/tcp
	firewall-cmd --permanent --add-port=2379-2380/tcp
	firewall-cmd --permanent --add-port=10250/tcp
	firewall-cmd --permanent --add-port=10251/tcp
	firewall-cmd --permanent --add-port=10252/tcp
	firewall-cmd --permanent --add-port=10255/tcp
	firewall-cmd --reload

	modprobe br_netfilter

	echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables

	cat <<EOF > /etc/yum.repos.d/kubernetes.repo
	[kubernetes]
	name=Kubernetes
	baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
	enabled=1
	gpgcheck=1
	repo_gpgcheck=1
	gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
       		https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
	EOF

 Configure docker:

	yum install docker kubectl kubelet kubeadm -y
	systemctl restart docker && systemctl enable docker
	systemctl  restart kubelet && systemctl enable kubelet
	swapoff -a
	systemctl daemon-reload

 Install dnsmasq:
	
	yum install dnsmasq -y
	cp /etc/resolv.conf ~/resolv.conf_bck
	rm -rf /etc/resolv.conf
	echo -e "nameserver 127.0.0.1\nnameserver $(hostname -i)" >> /etc/resolv.conf
	chmod 444 /etc/resolv.conf
	chattr +i /etc/resolv.conf
	echo -e "server=8.8.8.8\nserver=8.8.4.4" > /etc/dnsmasq.conf
	echo -e "$(hostname -i)\tlocalhost.$(hostname -d)" >> /etc/hosts
	service dnsmasq restart

 Initialize kubeadm:
	
	mkdir -p $HOME/.kube
	cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
	chown $(id -u):$(id -g) $HOME/.kube/config
	export kubever=$(kubectl version | base64 | tr -d '\n')
	kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$kubever"

 after kubeadm reset and init, to fix x509 cert error:

	sudo cp /etc/kubernetes/admin.conf $HOME/
	sudo chown $(id -u):$(id -g) $HOME/admin.conf
	export KUBECONFIG=$HOME/admin.conf

 Test cluster:
	
	kubeadm join 192.168.0.17:6443 --token 0i2m8j.3oe1yus8ex6zgrxc --discovery-token-ca-cert-hash sha256:e5d6b5c207dd55109cc0cdc069d6e567a199bea9f8972919018bc9c0b14efb2a

	sudo docker run -t a1b47cb4cf82 k8s-keystone-auth --tls-cert-file /home/apiserver.crt --tls-private-key-file /home/apiserver.key --keystone-policy-file examples/webhook/policy.json --keystone-url https://kaizen.massopen.cloud:5000/v3 &


 Cluster 4:

	kubeadm join 192.168.0.109:6443 --token 8vsj8d.3dm7twrbv8xrfchz --discovery-token-ca-cert-hash sha256:6744544b208b9a6bd431fc69ce0b063b99466729e77bcd6243e0eeafff93159d


Worker configuration:

 Install firewalld: 

	yum install firewalld -y
	systemctl start firewalld && systemctl enable firewalld
	firewall-cmd --permanent --add-port=10250/tcp
	firewall-cmd --permanent --add-port=10255/tcp
	firewall-cmd --permanent --add-port=30000-32767/tcp
	firewall-cmd --permanent --add-port=6783/tcp
	firewall-cmd --reload
	modprobe br_netfilter
	echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables

 	cat <<EOF > /etc/yum.repos.d/kubernetes.repo
	[kubernetes]
	name=Kubernetes
	baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
	enabled=1
	gpgcheck=1
	repo_gpgcheck=1
	gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        	https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
	EOF
 
 Install Docker and kubeadm:
	
	yum install docker kubeadm -y

	systemctl restart docker && systemctl enable docker

 cluster 2:
	
	kubeadm join --token e83d68.56fef47fa86febae 192.168.0.18:6443 --discovery-token-ca-cert-hash sha256:6c5ba92acda7b5f4b629d808633e8ebfa7fb9cecec2c09d9d1e0e877fe8d0050

 Cluster 3:
	
	kubeadm join --token fb8ba5.f2d0c610019a9d2b 192.168.0.111:6443 --discovery-token-ca-cert-hash sha256:c5e6a80f2d663ae9ef77b874941557cbfa331736c36ba58c0234ec3233d62d30


	
