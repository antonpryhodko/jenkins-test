```
sudo dnf install java-1.8.0-openjdk-devel epel-release  yum-utils
sudo dnf install daemonize
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install jenkins docker-ce docker-ce-cli containerd.io
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl start docker
sudo systemctl enable docker.service
sudo firewall-cmd --permanent --zone=public --add-port=8080/tcp
sudo firewall-cmd --reload
sudo groupadd docker
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
