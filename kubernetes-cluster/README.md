```
mkdir ~/.kube
scp root@kmaster.example.com:/etc/kubernetes/admin.conf ~/.kube/config

#enter password kubeadmin

sudo chown $(id -u):$(id -g) ~/.kube/config
export KUBECONFIG=~/.kube/config
echo "export KUBECONFIG=~/.kube/config" | tee -a ~/.bashrc

```
```
kubectl -n kube-system get pods -o wide

kubectl create -f dashboard/.

kubectl describe sa dashboard-admin -n kube-system

kubectl describe secret dashboard-admin-token-j4bcv -n kube-system

```

* copy token and login to worker node as https://kworker1:32323 and enter token

* open in another terminal
```
watch kubectl get all -o wide
```

```

kubectl create -f 1-nginx-pod.yaml
kubectl delete -f 1-nginx-pod.yaml

kubectl create -f 1-nginx-replicaset.yaml
kubectl delete pod/nginx-replicaset-2t2x9 # delete one of pods , it will create anotherone
kubectl delete replicaset nginx-replicaset


kubectl create -f 1-nginx-deployment.yaml
kubectl describe pod nginx-deploy-7cdbd8cdc9-6n5qf | less
kubectl describe replicaset nginx-deploy-7cdbd8cdc9 | less
```
* get info how many pods are running with lavel nginx

```
kubectl get pods -l run=nginx

```

* get pod info controlled by 
```
kubectl describe pod nginx-deploy-7cdbd8cdc9-6n5qf | grep -i controlled
```
* get replicaset info controlled by

```
kubectl describe replicaset nginx-deploy-7cdbd8cdc9 | grep -i controlled

```
* scale 3 replicas from 2 existing pods 

```
kubectl scale deploy nginx-deploy --replicas=3
```



# additional resources 

- [flannel-networking-demystify](https://msazure.club/flannel-networking-demystify/)

