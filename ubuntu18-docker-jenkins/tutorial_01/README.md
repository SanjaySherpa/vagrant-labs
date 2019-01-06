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

* Add `vagrant` user to `docker` group
```
sudo usermod -aG docker vagrant

newgrp docker

sudo service docker restart

docker ps # test docker is running or not


```

```
docker pull jenkins/jenkins:lts

make build run


```

* To confirm that the Java and Jenkins options are set correctly we can run ps in our container and see the running Jenkins Java process by using docker exec

```
docker exec jenkins-master ps -ef | grep java

```

* To get docker logs
```
docker cp jenkins-master:/var/log/jenkins/jenkins.log jenkins.log

cat jenkins.log

```