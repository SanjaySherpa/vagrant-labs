# jenkins master

```
sudo apt install software-properties-common apt-transport-https -y
sudo add-apt-repository ppa:openjdk-r/ppa -y

sudo apt install openjdk-8-jdk -y

sudo su
cd
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
echo 'deb https://pkg.jenkins.io/debian-stable binary/' | tee -a /etc/apt/sources.list

apt update
apt install jenkins -y

systemctl start jenkins
systemctl enable jenkins

cat /var/lib/jenkins/secrets/initialAdminPassword

```

```
su - jenkins

ssh-keygen


```
* Log in as root
* Edit ssh config: 
```
nano /etc/ssh/sshd_config
```
Change this line:
PasswordAuthentication no
to
PasswordAuthentication yes
Restart daemon:
``` 
systemctl restart sshd
```

# Setup Credentials on Jenkins

* And click the 'global' domain link.

* Now click 'Add Credentials'.

* Add Credentials

* Now choose the authentication method.

* Kind: SSH Username with private key
* Scope: Global
* Username: jenkins
* Private key: Enter directly and paste the 'id_rsa' private key of Jenkins user from the master server.
* Click 'OK'.

# Set up Slave Nodes

```
sudo apt install software-properties-common apt-transport-https -y
sudo add-apt-repository ppa:openjdk-r/ppa -y

sudo apt install openjdk-8-jdk -y

```

## Add New Jenkins User
Now add the 'Jenkins' user to all agent nodes.

```
sudo su
cd

useradd -m -s /bin/bash jenkins
passwd jenkins
```
* Log in as root
* Edit ssh config: 
```
nano /etc/ssh/sshd_config
```
Change this line:
PasswordAuthentication no
to
PasswordAuthentication yes
Restart daemon:
``` 
systemctl restart sshd
```

# Copy the SSH Key from Master to Slave
* Next, we need to upload the key 'id_rsa.pub' from the master to slave server nodes. We need to upload to each server nodes using 'ssh-copy-id' command as below.
```
su - jenkins

ssh-copy-id jenkins@172.42.42.102
```
Type the jenkins user password.

## Add New Slave Nodes
* On the Jenkins dashboard, click the 'Manage Jenkins' menu, and click 'Manage Nodes'.
* Click the 'New Node'.
* Type the node name 'ubuntuvm02', choose the 'permanent agent', and click 'OK'.

## Now type node information details.

Description: ubuntuvm02 node agent server
Remote root directory: /home/jenkins
Labels: ubuntuvm02
Launch method: Launch slave agent via SSH, type the host ip address '172.42.42.102', choose the authentication using 'Jenkins' credential.
Now click 'Save' button and wait for the master server to connect to all agent nodes and launch the agent services.

## Testing
Now we want to create a new simple build for Jenkins, and we want to execute the build on the bot 'ubuntuvm02' agent nodes.

On the Jenkins dashboard, click the 'New Item' menu.

Type the item name, choose the freestyle project, and click 'OK'.

On the general section, type the job description and check the 'Restrict where this project can be run' option.

On the 'Label Expression', specify the node such as 'ubuntuvm02'.

Move to the build section and choose the 'Execute shell' option, type the command as below.
```
top -b -n 1 | head -n 10 && hostname
```
Click 'Save' button, and you will be redirected to the job page.

Click the 'Build Now' to build the project, and then click item on the 'Build History' section.

And the following is my result.

Build on the 'ubuntuvm02' agent node.
