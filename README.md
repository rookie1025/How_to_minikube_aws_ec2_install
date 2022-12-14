# minikube_aws_ec2_install
install minikube on aws ec2 - refrence taken from internet

### Installing kubectl
### Run these commands as root
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl

```
------------------------------------------------------------------
```
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
------------------------------------------------------------------
### Install docker
```
sudo apt-get update && \
>     sudo apt-get install docker.io -y
```
------------------------------------------------------------------
### Installing minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
------------------------------------------------------------------
### Installing conntrack
```
sudo apt install conntrack -y
```
------------------------------------------------------------------
### Installing docker-shim.
```
git clone https://github.com/Mirantis/cri-dockerd.git
```
------------------------------------------------------------------
### Install GO###
```
wget https://storage.googleapis.com/golang/getgo/installer_linux
chmod +x ./installer_linux
./installer_linux
source ~/.bash_profile
```

```
cd cri-dockerd
mkdir bin
go get && go build -o bin/cri-dockerd
mkdir -p /usr/local/bin
install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
cp -a packaging/systemd/* /etc/systemd/system
sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
systemctl daemon-reload
systemctl enable cri-docker.service
systemctl enable --now cri-docker.socket
```

------------------------------------------------------------------

### Installing crictl:

### Using Curl:

```
VERSION="v1.24.1"
curl -L https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-${VERSION}-linux-amd64.tar.gz --output crictl-${VERSION}-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
```

### Using wget:
```
VERSION="v1.24.1"
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-$VERSION-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
```
------------------------------------------------------------------
### Starting minikube
```
minikube start --vm-driver=none
```
