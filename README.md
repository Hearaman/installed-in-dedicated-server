# installed-in-dedicated-server

##### Logged in to remote dedicated server using SSH

```bash
ssh username@ipaddress -p port_number
```

##### Updated ubuntu system
```bash
sudo apt-get update
sudo apt-get upgrade
```

## Install Apache2 Server
```bash
sudo apt install apache2 -y

# Enable apache2 (optional)
sudo systemctl enable apache2

# status check
sudo systemctl status apache2

# allow apache though firewall
sudo ufw allow 'Apache'

# allow apache though firewall (for HTTPS/SSL enabled)
sudo ufw allow 'Apache Full'
```

## Install Jenkins

Jenkins needs JDK17, so install JDK17 first.
```bash
sudo apt install openjdk-17-jdk -y

# Check java version
java --version
```

Follow below url to latest information and instructions guidelines about Jenkins
`https://www.jenkins.io/doc/book/installing/linux/`

Now, Install Jenkins

```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update

sudo apt-get install jenkins
```
By default, Jenkins uses port `8080` so use another port to run it, ex: `9090`

Change it in Jenkin config file `/lib/systemd/system/jenkins.service` (Not worked for me)
```bash
Environment="JENKINS_PORT=9090"
```
Sometime, modification will not come to effect. Please reload the demons

```bash
systemctl daemon-reload
```

If above configuration is not working, follow below step
```bash
sudo nano /etc/default/jenkins

# update & save
HTTP_POST=9090

systemctl daemon-reload
```

```bash
# enable server
sudo systemctl enable jenkins

# start
sudo systemctl start jenkins

# stop
sudo systemctl stop jenkins

# status
sudo systemctl status jenkins
```
Jenkins with new port need to be allowed at firewall.
```bash
sudo ufw allow 8080
sudo ufw status
```

Access jenkins `hostname_or_ip:port`
Execute below command for initial password
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword 
```


### Install Kubernetes

> **Note:** Kubernetes release candidate has been moved from `https://packages.cloud.google.com` to `pkgs.k8s.io`. 
**Executing bellow command may result errors.**
`curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-archive-keyring.gpg` and 
`echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list` 
**Error** 
Err:10 https://packages.cloud.google.com/apt kubernetes-xenial Release  404  Not Found [IP: 142.250.183.206 443]

```sh
# Add kubernetes Signing key
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# Add software repositories
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

# Update
sudo apt update
```

#### Install Kubernetes Tools
Each Kubernetes deployment consists of three separate tools:
- **Kubeadm:** A tool that initializes a Kubernetes cluster by fast-tracking the setup using community-sourced best practices.
- **Kubelet:** The work package that runs on every node and starts containers. The tool gives you command-line access to clusters.
- **Kubectl:** The command-line interface for interacting with clusters.

Execute the following commands on each server node to install the Kubernetes tools:

```sh
sudo apt install kubeadm kubelet kubectl
sudo apt-mark hold kubeadm kubelet kubectl

# Verify installation
kubeadm version
```


