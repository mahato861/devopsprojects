# Jnekins Server
https://transcripts.gotomeeting.com/#/s/9a366e5d362af2472e5a750fc71bb17c7d0d61145257670afcd0a8b6f783d0d4


Default java version in AWS Centos

```
java -version

```
java version "1.7.0_201"
OpenJDK Runtime Environment (amzn-2.6.16.0.78.amzn1-x86_64 u201-b00)
OpenJDK 64-Bit Server VM (build 24.201-b00, mixed mode)

```
sudo yum list | grep java-1.8

sudo yum install java-1.8.0-openjdk-devel.x86_64 -y

sudo update-alternatives --config java

```

There are 2 programs which provide 'java'.

  Selection    Command
-----------------------------------------------
*+ 1           /usr/lib/jvm/jre-1.7.0-openjdk.x86_64/bin/java
   2           /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/bin/java


```
Enter to keep the current selection[+], or type selection number: 2

```

```
java -version

```
update JAVA_HOME

```
nano .bash_profile

export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.191.b12-0.amzn2.x86_64/jre
export PATH=$PATH:$JAVA_HOME/bin

source .bash_profile

```
install jenkins

```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum install jenkins

sudo service jenkins start

```

Install Docker 

* Step 1: Create Yum Repo

```
sudo yum check-update

sudo yum update -y 

sudo nano /etc/yum.repos.d/docker.repo

[docker-repo]
Name=Docker Repository
Baseurl=https://yum.dockerproject.org/repo/main/centos/7/
enable=1
gpgcheck=1
gpgkey=https://yum.dockerproject.org/gpg

```

Step 2: Clean Yum Cache and Yum Update all Package

```
yum clean all

yum repolist

yum update

```

Step 3: Command to Install Docker-Engine and start docker on Amazon Linux

```
yum install docker-engine

systemctl enable docker

systemctl start docker

```

Step 4: Adding/providing ec2-user to docker group

```
sudo usermod -aG docker $(whoami)

sudo usermod -aG docker jenkins

sudo service jenkins restart

```

Install Apache Maven

```

cd /opt

sudo wget http://www-eu.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz

sudo tar xzf apache-maven-3.5.4-bin.tar.gz

sudo ln -s apache-maven-3.5.4 maven

sudo vi /etc/profile.d/maven.sh

export M2_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}

source /etc/profile.d/maven.sh

mvn -version

sudo rm -f /opt/apache-maven-3.5.4-bin.tar.gz

```
install git

```
sudo yum install git -y
```

# Application server

* Configure locale in ubuntu
```
curl -sL https://raw.githubusercontent.com/prabhatpankaj/ubuntustarter/master/initial.sh | sh
```

* Install Docker
```
sudo su

cd

curl -sSL https://get.docker.com/ | sh
```

* Create the docker group.
```
sudo groupadd docker
```
* Add the user to the docker group.
```
exit
sudo usermod -aG docker ubuntu
newgrp docker

```
*Log out and log back in to ensure docker runs with correct permissions.
Start docker.
```
sudo service docker start

docker ps
```

