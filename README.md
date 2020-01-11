# CKA
Preparation for Cloud Native Certified Kubernetes Administrator

- [Understanding Kubernetes Architecture](#understanding-kubernetes-architecture)
    - [Kubernetes Cluster Architecture](#kubernetes-cluster-architecture)
    - [Kubernetes API Primitives](#kubernetes-api-primitives)
    - [Kubernetes Services and Network Primitives](#kubernetes-services-and-network-primitives)

## Understanding Kubernetes Architecture
### Kubernetes Cluster Architecture
- The Kubernetes architecture has two main roles: the master role and the worker role.
    - You can have one or many **master** nodes
    - You can have zero or mane **worker** nodes

![img](https://github.com/Bes0n/CKA/blob/master/images/img1.png)

- Here what these components are used for:

![img](https://github.com/Bes0n/CKA/blob/master/images/img2.png)

Working with **kubectl**:

- ``` kubectl get nodes ``` - see your nodes
```
NAME       STATUS   ROLES    AGE   VERSION
minikube   Ready    master   64s   v1.17.0
```
  
- ``` kubectl get pods --all-namespaces ``` - see all pods running on all namespaces

```
NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
kube-system   coredns-6955765f44-dwqsq           1/1     Running   0          4m52s
kube-system   coredns-6955765f44-sfcxj           1/1     Running   0          4m52s
kube-system   etcd-minikube                      1/1     Running   0          4m59s
kube-system   kube-addon-manager-minikube        1/1     Running   0          4m58s
kube-system   kube-apiserver-minikube            1/1     Running   0          4m59s
kube-system   kube-controller-manager-minikube   1/1     Running   0          4m59s
kube-system   kube-proxy-zqvl8                   1/1     Running   0          4m52s
kube-system   kube-scheduler-minikube            1/1     Running   0          4m59s
kube-system   storage-provisioner                1/1     Running   0          4m50s
```

- ``` kubectl get pods --all-namespaces -o wide ``` - get detailed information about pods

- ```kubectl get namespaces``` - get your kubernetes **namespaces**
```
NAME              STATUS   AGE
default           Active   9m41s
kube-node-lease   Active   9m42s
kube-public       Active   9m42s
kube-system       Active   9m42s
```

This is how Application Running on Kubernetes looks like:

![img](https://github.com/Bes0n/CKA/blob/master/images/img3.png)

- Let's deploy simple POD with nginx image. JSON and YAML syntax accepted

```
cat << EOF | kubectl create -f -
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
EOF
```

### Kubernetes API Primitives
### Kubernetes Services and Network Primitives