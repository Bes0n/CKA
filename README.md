# CKA - Certified Kubernetes Administrator
Preparation for Cloud Native Certified Kubernetes Administrator

- [Understanding Kubernetes Architecture](#understanding-kubernetes-architecture)
    - [Kubernetes Cluster Architecture](#kubernetes-cluster-architecture)
    - [Kubernetes API Primitives](#kubernetes-api-primitives)
    - [Kubernetes Services and Network Primitives](#kubernetes-services-and-network-primitives)
    - [Exploring the Kubernetes Cluster via the Command Line](#exploring-the-kubernetes-cluster-via-the-command-line)
- [Building the Kubernetes Cluster](#building-the-kubernetes-cluster)
    - [Release Binaries, Provisioning, and Types of Clusters](#release-binaries-provisioning-and-types-of-clusters)
    - [Installing Kubernetes Master and Nodes](#installing-kubernetes-master-and-nodes)
    - [Building a Highly Available Kubernetes Cluster](#building-a-highly-available-kubernetes-cluster)
    - [Configuring Secure Cluster Communications](#configuring-secure-cluster-communications)
    - [Running End-to-End Tests on Your Cluster](#running-end-to-end-tests-on-your-cluster)
    - [Installing and Testing the Components of a Kubernetes Cluster](#installing-and-testing-the-components-of-a-kubernetes-cluster)
- [Managing the Kubernetes Cluster](#managing-the-kubernetes-cluster)
    - [Upgrading the Kubernetes Cluster](#upgrading-the-kubernetes-cluster)
    - [Operating System Upgrades within a Kubernetes Cluster](#operating-system-upgrades-within-a-kubernetes-cluster)
    - [Backing Up and Restoring a Kubernetes Cluster](#backing-up-and-restoring-a-kubernetes-cluster)
    - [Upgrading the Kubernetes Cluster Using kubeadm](#upgrading-the-kubernetes-cluster-using-kubeadm)
- [Cluster Communications](#cluster-communications)
    - [Pod and Node Networking](#pod-and-node-networking)
    - [Container Network Interface (CNI)](#container-network-interface-cni)
    - [Service Networking](#service-networking)
    - [Ingress Rules and Load Balancers](#ingress-rules-and-load-balancers)
    - [Cluster DNS](#cluster-dns)
    - [Creating a Service and Discovering DNS Names in Kubernetes](#creating-a-service-and-discovering-dns-names-in-kubernetes)
- [Pod Scheduling within the Kubernetes Cluster](#pod-scheduling-within-the-kubernetes-cluster)
    - [Configuring the Kubernetes Scheduler](#configuring-the-kubernetes-scheduler)
    - [Running Multiple Schedulers for Multiple Pods](#running-multiple-schedulers-for-multiple-pods)
    - [Scheduling Pods with Resource Limits and Label Selectors](#scheduling-pods-with-resource-limits-and-label-selectors)
    - [DaemonSets and Manually Scheduled Pods](#daemonsets-and-manually-scheduled-pods)
    - [Displaying Scheduler Events](#displaying-scheduler-events)
    - [Scheduling Pods with Taints and Tolerations in Kubernetes](#scheduling-pods-with-taints-and-tolerations-in-kubernetes)
- [Deploying Applications in the Kubernetes Cluster](#deploying-applications-in-the-kubernetes-cluster)
    - [Deploying an Application, Rolling Updates, and Rollbacks](#deploying-an-application-rolling-updates-and-rollbacks)
    - [Configuring an Application for High Availability and Scale](#configuring-an-application-for-high-availability-and-scale)
    - [Creating a Self-Healing Application](#creating-a-self-healing-application)
    - [Performing a Rolling Update of an Application in Kubernetes](#performing-a-rolling-update-of-an-application-in-kubernetes)
- [Managing Data in the Kubernetes Cluster](#managing-data-in-the-kubernetes-cluster)
    - [Persistent Volumes](#persistent-volumes)
    - [Volume Access Modes](#volume-access-modes)
    - [Persistent Volume Claims](#persistent-volume-claims)
    - [Storage Objects](#storage-objects)
    - [Applications with Persistent Storage](#applications-with-persistent-storage)
    - [Creating Persistent Storage for Pods in Kubernetes](#creating-persistent-storage-for-pods-in-kubernetes)
- [Securing the Kubernetes Cluster](#securing-the-kubernetes-cluster)
    - [Kubernetes Security Primitives](#kubernetes-security-primitives)
    - [Cluster Authentication and Authorization](#cluster-authentication-and-authorization)
    - [Configuring Network Policies](#configuring-network-policies)
    - [Creating TLS Certificates](#creating-tls-certificates)
    - [Secure Images](#secure-images)
    - [Defining Security Contexts](#defining-security-contexts)
    - [Securing Persistent Key Value Store](#securing-persistent-key-value-store)
    - [Creating a ClusterRole to Access a PV in Kubernetes](#creating-a-clusterrole-to-access-a-pv-in-kubernetes)
- [Monitoring Cluster Components](#monitoring-cluster-components)
    - [Monitoring the Cluster Components](#monitoring-the-cluster-components)
    - [Monitoring the Applications Running within a Cluster](#monitoring-the-applications-running-within-a-cluster)
    - [Managing Cluster Component Logs](#managing-cluster-component-logs)
    - [Managing Application Logs](#managing-application-logs)
    - [Monitor and Output Logs to a File in Kubernetes](#monitor-and-output-logs-to-a-file-in-kubernetes)
- [Identifying Failure within the Kubernetes Cluster](#identifying-failure-within-the-kubernetes-luster)
    - [Troubleshooting Application Failure](#troubleshooting-application-failure)
    - [Troubleshooting Control Plane Failure](#troubleshooting-control-plane-failure)
    - [Troubleshooting Worker Node Failure](#troubleshooting-worker-node-failure)
    - [Troubleshooting Networking](#troubleshooting-networking)
    - [Repairing Failed Pods in Kubernetes](#repairing-failed-pods-in-kubernetes)
- [Hands-On Practice Exam](#hands-on-practice-exam)
    - [CKA Practice Exam: Part 1](#cka-practice-exam-part-1)
    - [CKA Practice Exam: Part 2](#cka-practice-exam-part-2)
    - [CKA Practice Exam: Part 3](#cka-practice-exam-part-3)


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

- ``` kubectl get pods ``` - get information about pods
```
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          6m1s
```

- ``` kubectl describe pod nginx ``` - get detailed information about **nginx** pod
```
Name:         nginx
Namespace:    default
Priority:     0
Node:         minikube/192.168.99.100
Start Time:   Sat, 11 Jan 2020 13:18:18 +0100
Labels:       <none>
Annotations:  <none>
Status:       Running
IP:           172.17.0.4
IPs:
  IP:  172.17.0.4
Containers:
  nginx:
    Container ID:   docker://c072f93d7911a772f7fc09f35d6142abc0e730aa5f273b0f3e9d0615a16f282f
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:8aa7f6a9585d908a63e5e418dc5d14ae7467d2e36e1ab4f0d8f9d059a3d071ce
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 11 Jan 2020 13:18:28 +0100
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-b4lz9 (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  default-token-b4lz9:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-b4lz9
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  7m10s  default-scheduler  Successfully assigned default/nginx to minikube
  Normal  Pulling    7m8s   kubelet, minikube  Pulling image "nginx"
  Normal  Pulled     7m     kubelet, minikube  Successfully pulled image "nginx"
  Normal  Created    7m     kubelet, minikube  Created container nginx
  Normal  Started    7m     kubelet, minikube  Started container nginx
```

- ``` kubectl delete pod nginx ``` - delete your **nginx** pod

![img](https://github.com/Bes0n/CKA/blob/master/images/img4.png)

### Kubernetes API Primitives
Every component in the Kubernetes system makes a request to the API server. The kubectl command line utility processes those API calls for us and allows us to format our request in a certain way. In this lesson, we will learn how Kubernetes accepts the instructions to run deployments and go through the YAML script that is used to tell the control plane what our environment should look like.
  
- ```kubectl get componentstatus``` - get your components status 
```
NAME                 STATUS    MESSAGE             ERROR
scheduler            Healthy   ok
controller-manager   Healthy   ok
etcd-0               Healthy   {"health":"true"}
```

YAML file with configuration of nginx-deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

- ``` kubectl create -f nginx-deployment.yml ``` - create POD with configuration stored in **nginx-deployment.yml**

- ``` kubectl get deployment nginx-deployment -o yaml ``` - get information about your deployment in YAML format

- Definitions from YAML file:
    - **apiVersion** - Kubernetes API version, which indicates the path to ensure the API presents a clear, consistent view of system resources and behavior.
    - **kind** - Represents the kind of object you want to create. This is a required field. Examples of kinds of objects include pod, deployment, job, DaemonSet, ReplicaSet, ReplicationController, and more. 
    - **metadata** - Data that helpds uniquely identify the object, including a name string, UID, and optional namespace. 
    - **spec** - Describes your desired state for the object and the characteristics you want the object to have. The format of the object spec is different for every object and contains nested fields specific to that object. 
    - **spec (container)** - Specifies the pod's container image, volumes, and exposed ports for the container
    - **status** - Describes the actual state of the object and is supplied and updated by the Kubernetes system. At any given time, the Kubernetes Control Plane actively manages an object's actual state to match the desired state you supplied.

- ``` kubectl get pods --show-labels ``` - get your pod's labels
```
NAME                                READY   STATUS    RESTARTS   AGE    LABELS
nginx-deployment-54f57cf6bf-hddbx   1/1     Running   0          127m   app=nginx,pod-template-hash=54f57cf6bf
nginx-deployment-54f57cf6bf-wbw22   1/1     Running   0          127m   app=nginx,pod-template-hash=54f57cf6bf
```

- ```kubectl label pods nginx-deployment-54f57cf6bf-hddbx env=prod``` - add **prod** label to your pod
  
```
pod/nginx-deployment-54f57cf6bf-hddbx labeled
```
  
- ``` kubectl get pods -L env ``` - get pods with env label key
```
NAME                                READY   STATUS    RESTARTS   AGE    ENV
nginx-deployment-54f57cf6bf-hddbx   1/1     Running   0          135m   prod
nginx-deployment-54f57cf6bf-wbw22   1/1     Running   0          135m
```

- ``` kubectl annotate deployment nginx-deployment mysite.com/someannotation="isituseful" ``` - add additional annotation after deployment creation. 

- ``` kubectl get pods --field-selector status.phase=Running``` - filter objects based on some fields. In our case filter **pods** with phase status **running**

- ``` kubectl get services --field-selector metadata.namespace=default ``` - select services with default namespace

- ``` kubectl get pods --field-selector=status.phase=Running,metadata.namespace=default ``` - combination of two previous commands. 

- ``` kubectl get pods --field-selector=status.phase!=Running,metadata.namespace!=default ``` - reverve command, where status **is not** running and **not equal** to default namespace

By **label selectors** you can perform several actions on PODs which have these labels. You can edit, remove that labeled objects. 

![img](https://github.com/Bes0n/CKA/blob/master/images/img5.png)


### Kubernetes Services and Network Primitives
Kubernetes services allow you to dynamically access a group of replica pods without having to keep track of which pods are moved, changed, or deleted. In this lesson, we will go through how to create a service and communicate from one pod to another.

- ``` kubectl get pods -o wide``` - get wide information about pods.
```
NAME                                READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
nginx-deployment-54f57cf6bf-hddbx   1/1     Running   0          3h33m   172.17.0.5   minikube   <none>           <none>
nginx-deployment-54f57cf6bf-wbw22   1/1     Running   0          3h33m   172.17.0.4   minikube   <none>           <none>
```

- ``` kubectl delete pods nginx-deployment-54f57cf6bf-hddbx ``` - let's delete pod and see what will happen. 
```
NAME                                READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
nginx-deployment-54f57cf6bf-wbw22   1/1     Running   0          3h34m   172.17.0.4   minikube   <none>           <none>
nginx-deployment-54f57cf6bf-xlcdh   1/1     Running   0          18s     172.17.0.5   minikube   <none>           <none>
```

As a result we will have new pod running with new IP assigned on it. Here **service** takes place - dynamically access a group of replica pods without having to keep track of which pods are moved, changed, or deleted.
  
- Yaml file for creating **service** object looks like this:

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
  selector:
    app: nginx
```

- Where:
    - **kind** - type of deployment
    - **NodePort** - reservation of port for all nodes
    - **selector** - assign service to pod by selector, in our case by labels

- ``` kubectl create -f .\nginx-nodeport.yml``` - create service
- ``` kubectl get services ``` - get list of services 
- ``` kubectl get services nginx-nodeport ``` - get selected service - **nginx-nodeport**
```
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP        4h23m
nginx-nodeport   NodePort    10.96.241.16   <none>        80:30080/TCP   73s
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img6.png)

![img](https://github.com/Bes0n/CKA/blob/master/images/img7.png)

- ``` kubectl create -f .\busybox.yml ``` Let's create **busybox** pod

```
apiVersion: v1
kind: Pod
metadata:
  name: busybox
spec:
  containers:
  - name: busybox
    image: radial/busyboxplus:curl
    args:
    - sleep
    - "1000"
```

- ``` kubectl exec busybox -- curl 10.96.241.16:80 ``` - execute command from **busybox POD** to **NodePort service**. Here one POD reached another POD by using **kube-proxy**

![img](https://github.com/Bes0n/CKA/blob/master/images/img8.png)


### Exploring the Kubernetes Cluster via the Command Line
- LAB answers:
  - ``` kubectl get nodes ``` - List all the nodes in the cluster.
  - ``` kubectl get pods --all-namespaces ``` - List all the pods in all namespaces.
  - ``` kubectl get namespaces ``` - List all the namespaces in the cluster.
  - ``` kubectl get pods ``` - Check to see if there are any pods running in the default namespace.
  - ``` kubectl get pods --all-namespaces -o wide ``` - Find the IP address of the API server running on the master node.
  - ``` kubectl get deployments ``` - See if there are any deployments in this cluster.
  - ``` kubectl get pods --all-namespaces --show-labels -o wide ``` - Find the label applied to the etcd pod on the master node.


## Building the Kubernetes Cluster
### Release Binaries, Provisioning, and Types of Clusters
There are many choices when it comes to choosing where to create your Kubernetes cluster. In this lesson, we will focus on what you need to know for the CKA exam — specifically, how the cluster build relates to the types of clusters you will face in the exam.

![img](https://github.com/Bes0n/CKA/blob/master/images/img9.png)
  
![img](https://github.com/Bes0n/CKA/blob/master/images/img10.png)

### Installing Kubernetes Master and Nodes
Now that we’ve considered all the different types of clusters and where to locate the tools we need to install a cluster, let’s get to it! In this lesson, we will go through the all steps to install a three-node cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img11.png)

Get the Docker gpg key:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository:
```
sudo add-apt-repository    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Get the Kubernetes gpg key:
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

Add the Kubernetes repository:
```
cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

Update your packages:
```
sudo apt-get update
```

Install Docker, kubelet, kubeadm, and kubectl:
```
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.13.5-00 kubeadm=1.13.5-00 kubectl=1.13.5-00
```

Hold them at the current version:
```
sudo apt-mark hold docker-ce kubelet kubeadm kubectl
```

Add the iptables rule to **sysctl.conf**:
```
echo "net.bridge.bridge-nf-call-iptables=1" | sudo tee -a /etc/sysctl.conf
```

Enable iptables immediately:
```
sudo sysctl -p
```

Initialize the cluster (run only on the master):
```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

Set up local kubeconfig (only master node):
```
mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Apply Flannel CNI network overlay:
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

Join the worker nodes to the cluster:
```
sudo kubeadm join [your unique string from the kubeadm init command]
```

Verify the worker nodes have joined the cluster successfully:
```
kubectl get nodes
```

Compare this result of the kubectl get nodes command:
```
NAME                            STATUS   ROLES    AGE   VERSION
chadcrowell1c.mylabserver.com   Ready    master   4m18s v1.13.5
chadcrowell2c.mylabserver.com   Ready    none     82s   v1.13.5
chadcrowell3c.mylabserver.com   Ready    none     69s   v1.13.5
```

### Building a Highly Available Kubernetes Cluster
You can provide high availability for cluster components by running multiple instances — however, some replicated components must remain in standby mode. The scheduler and the controller manager are actively watching the cluster state and take action when it changes. If multiples are running, it creates the possibility of unwarranted duplicates of pods.

View the pods in the default namespace with a custom view:
```
kubectl get pods -o custom-columns=POD:metadata.name,NODE:spec.nodeName --sort-by spec.nodeName -n kube-system
```

View the kube-scheduler YAML (from that output you can see who is the current leader):
```
kubectl get endpoints kube-scheduler -n kube-system -o yaml
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img12.png)


Create a stacked etcd topology using kubeadm:
```
kubeadm init --config=kubeadm-config.yaml
```

Watch as pods are created in the default namespace:
```
kubectl get pods -n kube-system -w
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img13.png)


### Configuring Secure Cluster Communications
To prevent unauthorized users from modifying the cluster state, RBAC is used, defining roles and role bindings for a user. A service account resource is created for a pod to determine how it has control over the cluster state. For example, the default service account will not allow you to list the services in a namespace.

View the kube-config:
```
cat .kube/config | more
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img14.png)

View the service account token:
```
kubectl get secrets
```

Create a new namespace named **my-ns**:
```
kubectl create ns my-ns
```

Run the kube-proxy pod in the **my-ns** namespace:
```
kubectl run test --image=chadmcrowell/kubectl-proxy -n my-ns
```

List the pods in the **my-ns** namespace:
```
kubectl get pods -n my-ns
```

Run a shell in the newly created pod:
```
kubectl exec -it <name-of-pod> -n my-ns sh
```

List the services in the namespace via API call:
```
curl localhost:8001/api/v1/namespaces/my-ns/services
```

View the token file from within a pod:
```
cat /var/run/secrets/kubernetes.io/serviceaccount/token
```

List the service account resources in your cluster:
```
kubectl get serviceaccounts
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img15.png)

### Running End-to-End Tests on Your Cluster
Running end-to-end tests ensures your application will run efficiently without having to worry about cluster health problems. Kubetest is a useful tool for providing end-to-end tests — however, it is beyond the scope of this exam. In this lesson, we will go through the practice of testing our ability to run deployments, run pods, expose a container, execute a command from a container, run a service, and check the overall health of our nodes and pods for conditions.

![img](https://github.com/Bes0n/CKA/blob/master/images/img16.png)

Run a simple nginx deployment:
```
kubectl run nginx --image=nginx
```

View the deployments in your cluster:
```
kubectl get deployments
```

View the pods in the cluster:
```
kubectl get pods
```

Use port forwarding to access a pod directly:
```
kubectl port-forward $pod_name 8081:80
```

Get a response from the nginx pod directly:
```
curl --head http://127.0.0.1:8081
```

View the logs from a pod:
```
kubectl logs $pod_name
```

Run a command directly from the container:
```
kubectl exec -it nginx -- nginx -v
```

Create a service by exposing port 80 of the nginx deployment:
```
kubectl expose deployment nginx --port 80 --type NodePort
```

List the services in your cluster:
```
kubectl get services
```

Get a response from the service (run from worker node):
```
curl -I localhost:$node_port
```

List the nodes' status:
```
kubectl get nodes
```

View detailed information about the nodes:
```
kubectl describe nodes
```

View detailed information about the pods:
```
kubectl describe pods
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img17.png)

### Installing and Testing the Components of a Kubernetes Cluster

**Get the Docker gpg, and add it to your repository.**

- Run the following commands on all three nodes to get the Docker gpg key and add it to your repository:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

**Get the Kubernetes gpg key, and add it to your repository.**
- Run the following commands on all three nodes to get the Kubernetes gpg key and add it to your repository:
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat << EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

sudo apt-get update
```

**Install Docker, kubelet, kubeadm, and kubectl.**
- Run the following command on all three nodes to install docker, kubelet, kubeadm, and kubectl:
```
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu kubelet=1.13.5-00 kubeadm=1.13.5-00 kubectl=1.13.5-00

sudo apt-mark hold kubelet kubeadm kubectl docker-ce #mark installed applications to hold versions

```

**Initialize the Kubernetes cluster.**
- In the master node, run the following command to initialize the cluster using kubeadm:
```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

**Set up local kubeconfig.**
- In the master node, run the following commands to set up local kubeconfig:
```
mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

**Apply the flannel CNI plugin as a network overlay.**
- In the master node, run the following command to apply flannel:

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```

**Join the worker nodes to the cluster, and verify they have joined successfully.**
- In both of the worker nodes, run the output of the kubeadm init command to join the worker nodes to the cluster. Should look similar to:

```
sudo kubeadm join 'KUBERNETES_MASTER_IP':6443 --token 'UNIQUE_TOKEN' --discovery-token-ca-cert-hash sha256:'UNIQUE_HASH'
```

**Run a deployment that includes at least one pod, and verify it was successful.**
- In the master node, run the following commands to run a deployment of ngnix and verify:
```
kubectl create deployment nginx --image=nginx

kubectl get deployments
```

**Verify the pod is running and available.**
```
kubectl get pods

kubectl describe pods nginx-5c7588df-wgrg6
```

**Use port forwarding to extend port 80 to 8081, and verify access to the pod directly.**
- In the master node, run the following command to forward the container port 80 to 8081:
```
kubectl port-forward [pod_name] 8081:80
```

- Open a new shell to the Kubernetes master and run the following command:
```
curl --head http://127.0.0.1:8081
```

*NOTE: You must leave the previous session open in order to properly port forward. As soon as you close that session, the port will NO LONGER be open.*

**Execute a command directly on a pod.**
- In the original master node terminal, run this command to execute the **nginx version** command from a pod:
```
kubectl exec -it <pod_name> -- nginx -v
```

**Create a service, and verify connectivity on the node port.**
- In the original master node terminal, run the following commands to create a NodePort service and view the service:
```
kubectl expose deployment nginx --port 80 --type NodePort

kubectl get services
```

- In one of the worker node terminals, run the following command to verify its connectivity (get the **$node_port** number from the **PORT(S)** column of the above service output):

```
curl -I localhost:$node_port
```

## Managing the Kubernetes Cluster
### Upgrading the Kubernetes Cluster
kubeadm allows us to upgrade our cluster components in the proper order, making sure to include important feature upgrades we might want to take advantage of in the latest stable version of Kubernertes. In this lesson, we will go through upgrading our cluster from version 1.13.5 to 1.14.1.

![img](https://github.com/Bes0n/CKA/blob/master/images/img18.png)

Get the version of the API server:
```
kubectl version --short
```

View the version of kubelet:
```
kubectl describe nodes 
```

View the version of controller-manager pod:
```
kubectl get pod [controller_pod_name] -o yaml -n kube-system
```

Release the hold on versions of kubeadm and kubelet:
```
sudo apt-mark unhold kubelet kubeadm
```

Install version 1.14.1 of kubeadm:
```
sudo apt install -y kubeadm=1.14.1-00
```

Hold the version of kubeadm at 1.14.1:
```
sudo apt-mark hold kubeadm
```

Verify the version of kubeadm:
```
kubeadm version
```

Plan the upgrade of all the controller components:
```
sudo kubeadm upgrade plan
```

Upgrade the controller components:
```
sudo kubeadm upgrade apply v1.14.1
```

Release the hold on the version of kubectl:

```
sudo apt-mark unhold kubectl
```

Upgrade kubectl:
```
sudo apt install -y kubectl=1.14.1-00
```

Hold the version of kubectl at 1.14.1:
```
sudo apt-mark hold kubectl
```

Upgrade the version of kubelet:
```
sudo apt install -y kubelet=1.14.1-00
```

Hold the version of kubelet at 1.14.1:
```
sudo apt-mark hold kubelet
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img19.png)

### Operating System Upgrades within a Kubernetes Cluster
When we need to take a node down for maintenance, Kubernetes makes it easy to evict the pods on that node, take it down, and then continue scheduling pods after the maintenance is complete. Furthermore, if the node needs to be decommissioned, you can just as easily remove the node and replace it with a new one, joining it to the cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img20.png)

See which pods are running on which nodes:
```
kubectl get pods -o wide
```

Evict the pods on a node:
```
kubectl drain [node_name] --ignore-daemonsets
```

Watch as the node changes status:
```
kubectl get nodes -w
```

Schedule pods to the node after maintenance is complete:
```
kubectl uncordon [node_name]
```

Remove a node from the cluster:
```
kubectl delete node [node_name]
```

Generate a new token:
```
sudo kubeadm token generate
```

List the tokens:
```
sudo kubeadm token list
```


Print the kubeadm join command to join a node to the cluster:
```
sudo kubeadm token create [token_name] --ttl 2h --print-join-command
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img21.png)

### Backing Up and Restoring a Kubernetes Cluster
Backing up your cluster can be a useful exercise, especially if you have a single etcd cluster, as all the cluster state is stored there. The etcdctl utility allows us to easily create a snapshot of our cluster state (etcd) and save this to an external location. In this lesson, we’ll go through creating the snapshot and talk about restoring in the event of failure.

![img](https://github.com/Bes0n/CKA/blob/master/images/img22.png)

Get the etcd binaries:
```
wget https://github.com/etcd-io/etcd/releases/download/v3.3.12/etcd-v3.3.12-linux-amd64.tar.gz
```

Unzip the compressed binaries:
```
tar xvf etcd-v3.3.12-linux-amd64.tar.gz
```

Move the files into /usr/local/bin:
```
sudo mv etcd-v3.3.12-linux-amd64/etcd* /usr/local/bin
```

Take a snapshot of the etcd datastore using etcdctl:
```
sudo ETCDCTL_API=3 etcdctl snapshot save snapshot.db --cacert /etc/kubernetes/pki/etcd/server.crt --cert /etc/kubernetes/pki/etcd/ca.crt --key /etc/kubernetes/pki/etcd/ca.key
```

View the help page for etcdctl:
```
ETCDCTL_API=3 etcdctl --help
```

Browse to the folder that contains the certificate files:
```
cd /etc/kubernetes/pki/etcd/
```

View that the snapshot was successful:
```
ETCDCTL_API=3 etcdctl --write-out=table snapshot status snapshot.db
```

Zip up the contents of the etcd directory:
```
sudo tar -zcvf etcd.tar.gz /etc/kubernetes/pki/etcd
```

Copy the etcd directory to another server:
```
scp etcd.tar.gz cloud_user@18.219.235.42:~/
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img23.png)

### Upgrading the Kubernetes Cluster Using kubeadm
**Install Version 1.13.5 of kubeadm**

On the master node, check the current version of kubeadm.
```
kubectl get nodes
```

Create two new variables:
```
export VERSION=v1.13.5
export ARCH=amd64
```

Get the latest version of kubeadm.
```
curl -sSL https://dl.k8s.io/release/${VERSION}/bin/linux/${ARCH}/kubeadm > kubeadm
```

Install the latest version of kubeadm.
```
sudo install -o root -g root -m 0755 ./kubeadm /usr/bin/kubeadm
```

Verify that the installation was successful.
```
sudo kubeadm version
```

Plan the upgrade to check for errors.
```
sudo kubeadm upgrade plan
```

Apply the upgrade of the kube-scheduler and kube-controller-manager.
```
sudo kubeadm upgrade apply v1.13.5
```

**Install the Latest Version of kubelet on the Master Node**

Get the latest version of kubelet.
```
curl -sSL https://dl.k8s.io/release/${VERSION}/bin/linux/${ARCH}/kubelet > kubelet
```

Install the latest version of kubelet.
```
sudo install -o root -g root -m 0755 ./kubelet /usr/bin/kubelet
```

Restart the kubelet service.
```
sudo systemctl restart kubelet.service
```
Verify that the installation was successful.
```
kubectl get nodes
```

**Install the Latest Version of kubectl**

Create two new variables:
```
export VERSION=v1.13.5
export ARCH=amd64
```

Get the latest version of kubectl.
```
curl -sSL https://dl.k8s.io/release/${VERSION}/bin/linux/${ARCH}/kubectl > kubectl
```

Install the latest version of kubectl.
```
sudo install -o root -g root -m 0755 ./kubectl /usr/bin/kubectl
```

Verify that the installation was successful.
```
kubectl version
```

### Pod and Node Networking

Kubernetes keeps networking simple for effective communication between pods, even if they are located on a different node. In this lesson, we’ll talk about pod communication from within a node, including how to inspect the virtual interfaces, and then get into what happens when a pod wants to talk to another pod on a different node.

![img](https://github.com/Bes0n/CKA/blob/master/images/img24.png)

![img](https://github.com/Bes0n/CKA/blob/master/images/img25.png)

See which node our pod is on:
```
kubectl get pods -o wide
```

Log in to the node:
```
ssh [node_name]
```

View the node's virtual network interfaces:
```
ifconfig
```

View the containers in the pod:
```
docker ps
```

Get the process ID for the container:
```
docker inspect --format '{{ .State.Pid }}' [container_id]
```

Use nsenter to run a command in the process's network namespace:
```
nsenter -t [container_pid] -n ip addr
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img26.png)

### Container Network Interface (CNI)
A Container Network Interface (CNI) is an easy way to ease communication between containers in a cluster. The CNI has many responsibilities, including IP management, encapsulating packets, and mappings in userspace. In this lesson, we will cover the details of the Flannel CNI we used in our Linux Academy cluster and talk about the ways in which we simplified communication in our cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img27.png)

Apply the Flannel CNI plugin:
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml
```

### Service Networking
Services allow our pods to move around, get deleted, and replicate, all without having to manually keep track of their IP addresses in the cluster. This is accomplished by creating one gateway to distribute packets evenly across all pods. In this lesson, we will see the differences between a **NodePort** service and a **ClusterIP** service and see how the iptables rules take effect when traffic is coming in.

![img](https://github.com/Bes0n/CKA/blob/master/images/img28.png)

AML for the nginx NodePort service:
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
spec:
  type: NodePort
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 30080
  selector:
    app: nginx
```

Get the **services** YAML output for all the services in your cluster:
```
kubectl get services -o yaml
```

Try and ping the **clusterIP** service IP address:
```
ping 10.96.0.1
```

View the list of services in your cluster:
```
kubectl get services
```

View the list of endpoints in your cluster that get created with a service:
```
kubectl get endpoints
```

Look at the iptables rules for your services:
```
sudo iptables-save | grep KUBE | grep nginx
```

### Ingress Rules and Load Balancers
When handling traffic from outside sources, there are two ways to direct that traffic to your pods: deploying a load balancer, and creating an ingress controller and an Ingress resource. In this lesson, we will talk about the benefits of each and how Kubernetes distributes traffic to the pods on a node to reduce latency and direct traffic to the appropriate services within your cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img29.png)

View the list of services:
```
kubectl get services
```

The load balancer YAML spec:
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-loadbalancer
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: nginx
```

Create a new deployment:
```
kubectl run kubeserve2 --image=chadmcrowell/kubeserve2
```

View the list of deployments:
```
kubectl get deployments
```

Scale the deployments to 2 replicas:
```
kubectl scale deployment/kubeserve2 --replicas=2
```

View which pods are on which nodes:
```
kubectl get pods -o wide
```

Create a load balancer from a deployment:
```
kubectl expose deployment kubeserve2 --port 80 --target-port 8080 --type LoadBalancer
```

View the services in your cluster:
```
kubectl get services
```

Watch as an external port is created for a service:
```
kubectl get services -w
```

Look at the YAML for a service:
```
kubectl get services kubeserve2 -o yaml
```

Curl the external IP of the load balancer:
```
curl http://[external-ip]
```

View the annotation associated with a service:
```
kubectl describe services kubeserve
```

Set the annotation to route load balancer traffic local to the node:
```
kubectl annotate service kubeserve2 externalTrafficPolicy=Local
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img30.png)

The YAML for an Ingress resource:
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: service-ingress
spec:
  rules:
  - host: kubeserve.example.com
    http:
      paths:
      - backend:
          serviceName: kubeserve2
          servicePort: 80
  - host: app.example.com
    http:
      paths:
      - backend:
          serviceName: nginx
          servicePort: 80
  - http:
      paths:
      - backend:
          serviceName: httpd
          servicePort: 80
```

Edit the ingress rules:
```
kubectl edit ingress
```

View the existing ingress rules:
```
kubectl describe ingress
```

Curl the hostname of your Ingress resource:
```
curl http://kubeserve2.example.com
```

### Cluster DNS
CoreDNS is now the new default DNS plugin for Kubernetes. In this lesson, we’ll go over the hostnames for pods and services. We will also discover how you can customize DNS to include your own nameservers.

![img](https://github.com/Bes0n/CKA/blob/master/images/img31.png)

View the CoreDNS pods in the **kube-system** namespace:
```
kubectl get pods -n kube-system
```

View the CoreDNS deployment in your Kubernetes cluster:
```
kubectl get deployments -n kube-system
```

View the service that performs load balancing for the DNS server:
```
kubectl get services -n kube-system
```

Spec for the busybox pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox:1.28.4
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
```

View the resolv.conf file that contains the nameserver and search in DNS:
```
kubectl exec -it busybox -- cat /etc/resolv.conf
```

Look up the DNS name for the native Kubernetes service:
```
kubectl exec -it busybox -- nslookup kubernetes
```

Look up the DNS names of your pods:
```
kubectl exec -ti busybox -- nslookup [pod-ip-address].default.pod.cluster.local
```

Look up a service in your Kubernetes cluster:
```
kubectl exec -it busybox -- nslookup kube-dns.kube-system.svc.cluster.local
```

Get the logs of your CoreDNS pods:
```
kubectl logs [coredns-pod-name]
```

YAML spec for a headless service:
```
apiVersion: v1
kind: Service
metadata:
  name: kube-headless
spec:
  clusterIP: None
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: kubserve2
```

YAML spec for a custom DNS pod:
```
apiVersion: v1
kind: Pod
metadata:
  namespace: default
  name: dns-example
spec:
  containers:
    - name: test
      image: nginx
  dnsPolicy: "None"
  dnsConfig:
    nameservers:
      - 8.8.8.8
    searches:
      - ns1.svc.cluster.local
      - my.dns.search.suffix
    options:
      - name: ndots
        value: "2"
      - name: edns0
```

### Creating a Service and Discovering DNS Names in Kubernetes
**Create an nginx deployment using the latest nginx image.**
- Use this command to create an nginx deployment:
```
kubectl run nginx --image=nginx
```

**Verify the deployment has been created successfully.**
- Use this command to verify deployment was successful:
```
kubectl get deployments
```

**Create a service from the nginx deployment created in the previous objective.**
- Use this command to create a service:
```
kubectl expose deployment nginx --port 80 --type NodePort
```

- Use this command to verify the service was created:
```
kubectl get services
```

**Create a pod that will allow you to perform the DNS query.**
- Use the following YAML to create the busybox pod spec:
```
apiVersion: v1
kind: Pod
metadata:
  name: busybox
spec:
  containers:
  - image: busybox:1.28.4
    command:
      - sleep
      - "3600"
    name: busybox
  restartPolicy: Always
```

- Use the following command to create the busybox pod:
```
kubectl create -f busybox.yaml
```

- Use the following command to verify the pod was created successfully:
```
kubectl get pods
```

**Perform the DNS query to the service created in an earlier objective.**
- Use the following command to query the DNS name of the nginx service:
```
kubectl exec busybox -- nslookup nginx
```

**Record the DNS name of the service.**
- Record the name of:
```
<service-name>.default.svc.cluster.local
```

## Pod Scheduling within the Kubernetes Cluster
### Configuring the Kubernetes Scheduler
The default scheduler in Kubernetes attempts to find the best node for your pod by going through a series of steps. In this lesson, we will cover the steps in detail in order to better understand the scheduler’s function when placing pods on nodes to maximize uptime for the applications running in your cluster. We will also go through how to create a deployment with node affinity.

![img](https://github.com/Bes0n/CKA/blob/master/images/img32.png)

Label your node as being located in availability zone 1:
```
kubectl label node chadcrowell1c.mylabserver.com availability-zone=zone1
```

Label your node as dedicated infrastructure:
```
kubectl label node chadcrowell2c.mylabserver.com share-type=dedicated
```

Here is the YAML for the deployment to include the node affinity rules:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pref
spec:
  replicas: 5
  template:
    metadata:
      labels:
        app: pref
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 80
            preference:
              matchExpressions:
              - key: availability-zone
                operator: In
                values:
                - zone1
          - weight: 20
            preference:
              matchExpressions:
              - key: share-type
                operator: In
                values:
                - dedicated
      containers:
      - args:
        - sleep
        - "99999"
        image: busybox
        name: main
```

Create the deployment:
```
kubectl create -f pref-deployment.yaml
```

View the deployment:
```
kubectl get deployments
```

View which pods landed on which nodes:
```
kubectl get pods -o wide
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img33.png)

### Running Multiple Schedulers for Multiple Pods
In Kubernetes, you can run multiple schedulers simultaneously. You can then use different schedulers to schedule different pods. You may, for example, want to set different rules for the scheduler to run all of your pods on one node. In this lesson, I will show you how to deploy a new scheduler alongside your default scheduler and then schedule three different pods using the two schedulers.

![img](https://github.com/Bes0n/CKA/blob/master/images/img34.png)

**ClusterRole.yaml**
```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: csinodes-admin
rules:
- apiGroups: ["storage.k8s.io"]
  resources: ["csinodes"]
  verbs: ["get", "watch", "list"]
```

**ClusterRoleBinding.yaml**
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-csinodes-global
subjects:
- kind: ServiceAccount
  name: my-scheduler
  namespace: kube-system
roleRef:
  kind: ClusterRole
  name: csinodes-admin
  apiGroup: rbac.authorization.k8s.io
```

**Role.yaml**
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: system:serviceaccount:kube-system:my-scheduler
  namespace: kube-system
rules:
- apiGroups:
  - storage.k8s.io
  resources:
  - csinodes
  verbs:
  - get
  - list
  - watch
```

**RoleBinding.yaml**
```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-csinodes
  namespace: kube-system
subjects:
- kind: User
  name: kubernetes-admin
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role 
  name: system:serviceaccount:kube-system:my-scheduler
  apiGroup: rbac.authorization.k8s.io
```

Edit the existing kube-scheduler cluster role with **kubectl edit clusterrole system:kube-scheduler** and add the following:
```
- apiGroups:
  - ""
  resourceNames:
  - kube-scheduler
  - my-scheduler
  resources:
  - endpoints
  verbs:
  - delete
  - get
  - patch
  - update
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - watch
  - list
  - get
```

**My-scheduler.yaml**
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: my-scheduler
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: my-scheduler-as-kube-scheduler
subjects:
- kind: ServiceAccount
  name: my-scheduler
  namespace: kube-system
roleRef:
  kind: ClusterRole
  name: system:kube-scheduler
  apiGroup: rbac.authorization.k8s.io
---
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    component: scheduler
    tier: control-plane
  name: my-scheduler
  namespace: kube-system
spec:
  selector:
    matchLabels:
      component: scheduler
      tier: control-plane
  replicas: 1
  template:
    metadata:
      labels:
        component: scheduler
        tier: control-plane
        version: second
    spec:
      serviceAccountName: my-scheduler
      containers:
      - command:
        - /usr/local/bin/kube-scheduler
        - --address=0.0.0.0
        - --leader-elect=false
        - --scheduler-name=my-scheduler
        image: chadmcrowell/custom-scheduler
        livenessProbe:
          httpGet:
            path: /healthz
            port: 10251
          initialDelaySeconds: 15
        name: kube-second-scheduler
        readinessProbe:
          httpGet:
            path: /healthz
            port: 10251
        resources:
          requests:
            cpu: '0.1'
        securityContext:
          privileged: false
        volumeMounts: []
      hostNetwork: false
      hostPID: false
      volumes: []
```

Run the deployment for **my-scheduler**:
```
kubectl create -f my-scheduler.yaml
```

View your new scheduler in the **kube-system** namespace:
```
kubectl get pods -n kube-system
```

**pod1.yaml**
```
apiVersion: v1
kind: Pod
metadata:
  name: no-annotation
  labels:
    name: multischeduler-example
spec:
  containers:
  - name: pod-with-no-annotation-container
    image: k8s.gcr.io/pause:2.0
```

**pod2.yaml**
```
apiVersion: v1
kind: Pod
metadata:
  name: annotation-default-scheduler
  labels:
    name: multischeduler-example
spec:
  schedulerName: default-scheduler
  containers:
  - name: pod-with-default-annotation-container
    image: k8s.gcr.io/pause:2.0
```

**pod3.yaml**
```
apiVersion: v1
kind: Pod
metadata:
  name: annotation-second-scheduler
  labels:
    name: multischeduler-example
spec:
  schedulerName: my-scheduler
  containers:
  - name: pod-with-second-annotation-container
    image: k8s.gcr.io/pause:2.0
```

Create pods:
```
kubectl create -f pod1.yaml #pod2.yaml pod3.yaml
```

View the pods as they are created:
```
kubectl get pods -o wide
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img35.png)

### Scheduling Pods with Resource Limits and Label Selectors
In order to share the resources of your node properly, you can set resource limits and requests in Kubernetes. This allows you to reserve enough CPU and memory for your application while still maintaining system health. In this lesson, we will create some requests and limits in our pod YAML to show how it’s used by the node.

![img](https://github.com/Bes0n/CKA/blob/master/images/img36.png)

View the capacity and the allocatable info from a node:
```
kubectl describe nodes
```

The pod YAML for a pod with requests:
```
apiVersion: v1
kind: Pod
metadata:
  name: resource-pod1
spec:
  nodeSelector:
    kubernetes.io/hostname: "chadcrowell3c.mylabserver.com"
  containers:
  - image: busybox
    command: ["dd", "if=/dev/zero", "of=/dev/null"]
    name: pod1
    resources:
      requests:
        cpu: 800m
        memory: 20Mi
```

Create the requests pod:
```
kubectl create -f resource-pod1.yaml
```

View the pods and nodes they landed on:
```
kubectl get pods -o wide
```

The YAML for a pod that has a large request:
```
apiVersion: v1
kind: Pod
metadata:
  name: resource-pod2
spec:
  nodeSelector:
    kubernetes.io/hostname: "chadcrowell3c.mylabserver.com"
  containers:
  - image: busybox
    command: ["dd", "if=/dev/zero", "of=/dev/null"]
    name: pod2
    resources:
      requests:
        cpu: 1000m
        memory: 20Mi
```

Create the pod with 1000 millicore request:
```
kubectl create -f resource-pod2.yaml
```

See why the pod with a large request didn’t get scheduled:
```
kubectl describe resource-pod2
```

Look at the total requests per node:
```
kubectl describe nodes chadcrowell3c.mylabserver.com
```

Delete the first pod to make room for the pod with a large request:
```
kubectl delete pods resource-pod1
```

Watch as the first pod is terminated and the second pod is started:
```
kubectl get pods -o wide -w
```

The YAML for a pod that has limits:
```
apiVersion: v1
kind: Pod
metadata:
  name: limited-pod
spec:
  containers:
  - image: busybox
    command: ["dd", "if=/dev/zero", "of=/dev/null"]
    name: main
    resources:
      limits:
        cpu: 1
        memory: 20Mi
```

Create a pod with limits:
```
kubectl create -f limited-pod.yaml
```

Use the exec utility to use the top command:
```
kubectl exec -it limited-pod top
```

Notes:
  - Request resources - can consume all available resources on a node.
  - Limits resources - pods will not consume that set limits. But if you set more than node can provide kubernetes will kill that pod
  - Using top command from pod will show you resources of pod, but node's resources.  

![img](https://github.com/Bes0n/CKA/blob/master/images/img37.png)


### DaemonSets and Manually Scheduled Pods
DaemonSets do not use a scheduler to deploy pods. In fact, there are currently DaemonSets in the Kubernetes cluster that we made. In this lesson, I will show you where to find those and how to create your own DaemonSet pods to deploy without the need for a scheduler.

![img](https://github.com/Bes0n/CKA/blob/master/images/img38.png)

Find the DaemonSet pods that exist in your kubeadm cluster:
```
kubectl get pods -n kube-system -o wide
```

Delete a DaemonSet pod and see what happens:
```
kubectl delete pods [pod_name] -n kube-system
```

Give the node a label to signify it has SSD:
```
kubectl label node [node_name] disk=ssd
```

The YAML for a DaemonSet:
```
apiVersion: apps/v1beta2
kind: DaemonSet
metadata:
  name: ssd-monitor
spec:
  selector:
    matchLabels:
      app: ssd-monitor
  template:
    metadata:
      labels:
        app: ssd-monitor
    spec:
      nodeSelector:
        disk: ssd
      containers:
      - name: main
        image: linuxacademycontent/ssd-monitor
```

Create a DaemonSet from a YAML spec:
```
kubectl create -f ssd-monitor.yaml
```

Label another node to specify it has SSD:
```
kubectl label node chadcrowell2c.mylabserver.com disk=ssd
```

View the DaemonSet pods that have been deployed:
```
kubectl get pods -o wide
```

Remove the label from a node and watch the DaemonSet pod terminate:
```
kubectl label node chadcrowell3c.mylabserver.com disk-
```

Change the label on a node to change it to spinning disk:
```
kubectl label node chadcrowell2c.mylabserver.com disk=hdd --overwrite
```

Pick the label to choose for your DaemonSet:
```
kubectl get nodes chadcrowell3c.mylabserver.com --show-labels
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img39.png)

### Displaying Scheduler Events
There are multiple ways to view the events related to the scheduler. In this lesson, we’ll look at ways in which you can troubleshoot any problems with your scheduler or just find out more information.

![img](https://github.com/Bes0n/CKA/blob/master/images/img40.png)

View the name of the scheduler pod:
```
kubectl get pods -n kube-system
```

Get the information about your scheduler pod events:
```
kubectl describe pods [scheduler_pod_name] -n kube-system
```

View the events in your default namespace:
```
kubectl get events
```

View the events in your kube-system namespace:
```
kubectl get events -n kube-system
```

Delete all the pods in your default namespace:
```
kubectl delete pods --all
```

Watch events as they are appearing in real time:
```
kubectl get events -w
```

View the logs from the scheduler pod:
```
kubectl logs [kube_scheduler_pod_name] -n kube-system
```

The location of a systemd service scheduler pod:
```
/var/log/kube-scheduler.log
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img41.png)

### Scheduling Pods with Taints and Tolerations in Kubernetes

**Taint one of the worker nodes to repel work.**
- Use the following command to taint the node:
```
kubectl taint node <node_name> node-type=prod:NoSchedule
```

**Schedule a pod to the dev environment.**
- Use the following YAML to specify a pod that will be scheduled to the dev environment:
```
apiVersion: v1
kind: Pod
metadata:
 name: dev-pod
 labels:
   app: busybox
spec:
 containers:
 - name: dev
   image: busybox
   command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```

- Use the following command to create the pod:
```
kubectl create -f dev-pod.yaml
```

**Allow a pod to be scheduled to the prod environment.**
- Use the following YAML to create a deployment and a pod that will tolerate the prod environment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
 name: prod
spec:
 replicas: 1
 selector:
   matchLabels:
     app: prod
 template:
   metadata:
     labels:
       app: prod
   spec:
     containers:
     - args:
       - sleep
       - "3600"
       image: busybox
       name: main
     tolerations:
     - key: node-type
       operator: Equal
       value: prod
       effect: NoSchedule
```

- Use the following command to create the pod:
```
kubectl create -f prod-deployment.yaml
```

**Verify each pod has been scheduled and verify the toleration.**
- Use the following command to verify the pods have been scheduled:

```
kubectl get pods -o wide
```

- Verify the toleration of the production pod:
```
kubectl get pods <pod_name> -o yaml
```

## Deploying Applications in the Kubernetes Cluster
### Deploying an Application, Rolling Updates, and Rollbacks
We already know Kubernetes will run pods and deployments, but what happens when you need to update or change the version of your application running inside of the Kubernetes cluster? That’s where rolling updates come in, allowing you to update the app image with zero downtime. In this lesson, we’ll go over a rolling update, how to roll back, and how to pause the update if things aren’t going well.

![img](https://github.com/Bes0n/CKA/blob/master/images/img42.png)

The YAML for a deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubeserve
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kubeserve
  template:
    metadata:
      name: kubeserve
      labels:
        app: kubeserve
    spec:
      containers:
      - image: linuxacademycontent/kubeserve:v1
        name: app
```

Create a deployment with a record (for rollbacks):
```
kubectl create -f kubeserve-deployment.yaml --record
```

Check the status of the rollout:
```
kubectl rollout status deployments kubeserve
```

View the ReplicaSets in your cluster:
```
kubectl get replicasets
```

Scale up your deployment by adding more replicas:
```
kubectl scale deployment kubeserve --replicas=5
```

Expose the deployment and provide it a service:
```
kubectl expose deployment kubeserve --port 80 --target-port 80 --type NodePort
```

Set the minReadySeconds attribute to your deployment:
```
kubectl patch deployment kubeserve -p '{"spec": {"minReadySeconds": 10}}'
```

Use kubectl apply to update a deployment:
```
kubectl apply -f kubeserve-deployment.yaml
```

Use kubectl replace to replace an existing deployment:
```
kubectl replace -f kubeserve-deployment.yaml
```

Run this curl look while the update happens:
```
while true; do curl http://10.105.31.119; done
```

Perform the rolling update:
```
kubectl set image deployments/kubeserve app=linuxacademycontent/kubeserve:v2 --v 6
```

Describe a certain ReplicaSet:
```
kubectl describe replicasets kubeserve-[hash]
```

Apply the rolling update to version 3 (buggy):
```
kubectl set image deployment kubeserve app=linuxacademycontent/kubeserve:v3
```

Undo the rollout and roll back to the previous version:
```
kubectl rollout undo deployments kubeserve
```

Look at the rollout history:
```
kubectl rollout history deployment kubeserve
```

Roll back to a certain revision:
```
kubectl rollout undo deployment kubeserve --to-revision=2
```

Pause the rollout in the middle of a rolling update (canary release):
```
kubectl rollout pause deployment kubeserve
```

Resume the rollout after the rolling update looks good:
```
kubectl rollout resume deployment kubeserve
```

Notes:
  - difference between ```kubectl replace``` and ```kubectl apply``` is
    - in **apply** if deployment doesn't exist it will be created and applied
    - in **replace** deployment must exist, otherwise deployment will fail

![img](https://github.com/Bes0n/CKA/blob/master/images/img43.png)

### Configuring an Application for High Availability and Scale
Continuing from the last lesson, we will go through how Kubernetes will save you from EVER releasing code with bugs. Then, we will talk about ConfigMaps and secrets as a way to pass configuration data to your apps.

![img](https://github.com/Bes0n/CKA/blob/master/images/img44.png)

The YAML for a readiness probe:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubeserve
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kubeserve
  minReadySeconds: 10
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
    type: RollingUpdate
  template:
    metadata:
      name: kubeserve
      labels:
        app: kubeserve
    spec:
      containers:
      - image: linuxacademycontent/kubeserve:v3
        name: app
        readinessProbe:
          periodSeconds: 1
          httpGet:
            path: /
            port: 80
```

Apply the readiness probe:
```
kubectl apply -f kubeserve-deployment-readiness.yaml
```

View the rollout status:
```
kubectl rollout status deployment kubeserve
```

Describe deployment:
```
kubectl describe deployment
```

Create a ConfigMap with two keys:
```
kubectl create configmap appconfig --from-literal=key1=value1 --from-literal=key2=value2
```

Get the YAML back out from the ConfigMap:
```
kubectl get configmap appconfig -o yaml
```

The YAML for the ConfigMap pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-pod
spec:
  containers:
  - name: app-container
    image: busybox:1.28
    command: ['sh', '-c', "echo $(MY_VAR) && sleep 3600"]
    env:
    - name: MY_VAR
      valueFrom:
        configMapKeyRef:
          name: appconfig
          key: key1
```

Create the pod that is passing the ConfigMap data:
```
kubectl apply -f configmap-pod.yaml
```

Get the logs from the pod displaying the value:
```
kubectl logs configmap-pod
```

The YAML for a pod that has a ConfigMap volume attached:
```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-volume-pod
spec:
  containers:
  - name: app-container
    image: busybox
    command: ['sh', '-c', "echo $(MY_VAR) && sleep 3600"]
    volumeMounts:
      - name: configmapvolume
        mountPath: /etc/config
  volumes:
    - name: configmapvolume
      configMap:
        name: appconfig
```

Create the ConfigMap volume pod:
```
kubectl apply -f configmap-volume-pod.yaml
```

Get the keys from the volume on the container:
```
kubectl exec configmap-volume-pod -- ls /etc/config
```

Get the values from the volume on the pod:
```
kubectl exec configmap-volume-pod -- cat /etc/config/key1
```

The YAML for a secret:
```
apiVersion: v1
kind: Secret
metadata:
  name: appsecret
stringData:
  cert: value
  key: value
```

Create the secret:
```
kubectl apply -f appsecret.yaml
```

The YAML for a pod that will use the secret:
```
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod
spec:
  containers:
  - name: app-container
    image: busybox
    command: ['sh', '-c', "echo Hello, Kubernetes! && sleep 3600"]
    env:
    - name: MY_CERT
      valueFrom:
        secretKeyRef:
          name: appsecret
          key: cert
```

Create the pod that has attached secret data:
```
kubectl apply -f secret-pod.yaml
```

Open a shell and echo the environment variable:
```
kubectl exec -it secret-pod -- sh
echo $MY_CERT
```

The YAML for a pod that will access the secret from a volume:
```
apiVersion: v1
kind: Pod
metadata:
  name: secret-volume-pod
spec:
  containers:
  - name: app-container
    image: busybox
    command: ['sh', '-c', "echo $(MY_VAR) && sleep 3600"]
    volumeMounts:
      - name: secretvolume
        mountPath: /etc/certs
  volumes:
    - name: secretvolume
      secret:
        secretName: appsecret
```

Create the pod with volume attached with secrets:
```
kubectl apply -f secret-volume-pod.yaml
```

Get the keys from the volume mounted to the container with the secrets:
```
kubectl exec secret-volume-pod -- ls /etc/certs
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img45.png)

### Creating a Self-Healing Application
In this lesson, we’ll go through the power of ReplicaSets, which make your application self-healing by replicating pods and moving them around and spinning them up when nodes fail. We’ll also talk about StatefulSets and the benefit they provide.

![img](https://github.com/Bes0n/CKA/blob/master/images/img46.png)

The YAML for a ReplicaSet:
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myreplicaset
  labels:
    app: app
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: main
        image: linuxacademycontent/kubeserve
```

Create the ReplicaSet:
```
kubectl apply -f replicaset.yaml
```

The YAML for a pod with the same label as a ReplicaSet:
```
apiVersion: v1
kind: Pod
metadata:
  name: pod1
  labels:
    tier: frontend
spec:
  containers:
  - name: main
    image: linuxacademycontent/kubeserve
```

Create the pod with the same label:
```
kubectl apply -f pod-replica.yaml
```

Watch the pod get terminated:
```
kubectl get pods -w 
```

The YAML for a StatefulSet:
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
          name: web
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

Create the StatefulSet:
```
kubectl apply -f statefulset.yaml
```

View all StatefulSets in the cluster:
```
kubectl get statefulsets
```

Describe the StatefulSets:
```
kubectl describe statefulsets
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img47.png)

### Performing a Rolling Update of an Application in Kubernetes
**Create and roll out version 1 of the application, and verify a successful deployment.**
- Use the following YAML named kubeserve-deployment.yaml to create your deployment:
```
 apiVersion: apps/v1
 kind: Deployment
 metadata:
   name: kubeserve
 spec:
   replicas: 3
   selector:
     matchLabels:
       app: kubeserve
   template:
     metadata:
       name: kubeserve
       labels:
         app: kubeserve
     spec:
       containers:
       - image: linuxacademycontent/kubeserve:v1
         name: app
```

- Use the following command to create the deployment:
```
 kubectl apply -f kubeserve-deployment.yaml --record
```

- Use the following command to verify the deployment was successful:
```
 kubectl rollout status deployments kubeserve
```

- Use the following command to verify the app is at the correct version:
```
 kubectl describe deployment kubeserve
```

**Scale up the application to create high availability.**
- Use the following command to scale up your application to five replicas:
```
kubectl scale deployment kubeserve --replicas=5
```
- Use the following command to verify the additional replicas have been created:
```
kubectl get pods
```

**Create a service, so users can access the application.**
- Use the following command to create a service for your deployment:
```
kubectl expose deployment kubeserve --port 80 --target-port 80 --type NodePort
```

- Use the following command to verify the service is present and collect the cluster IP:
```
kubectl get services
```

- Use the following command to verify the service is responding:
```
curl http://<ip-address-of-the-service>
```

**Perform a rolling update to version 2 of the application, and verify its success.**
- Use this curl loop command to see the version change as you perform the rolling update:
```
 while true; do curl http://<ip-address-of-the-service>; done
```
- Use this command to perform the update (while the curl loop is running):
```
 kubectl set image deployments/kubeserve app=linuxacademycontent/kubeserve:v2 --v 6
```

- Use this command to view the additional ReplicaSet created during the update:
```
 kubectl get replicasets
```
- Use this command to verify all pods are up and running:
```
 kubectl get pods
```

- Use this command to view the rollout history:
```
 kubectl rollout history deployment kubeserve
```

## Managing Data in the Kubernetes Cluster
### Persistent Volumes
In Kubernetes, pods are ephemeral. This creates a unique challenge with attaching storage directly to the filesystem of a container. Persistent Volumes are used to create an abstraction layer between the application and the underlying storage, making it easier for the storage to follow the pods as they are deleted, moved, and created within your Kubernetes cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img48.png)

In the Google Cloud Engine, find the region your cluster is in:
```
gcloud container clusters list
```

Using Google Cloud, create a persistent disk in the same region as your cluster:
```
gcloud compute disks create --size=1GiB --zone=us-central1-a mongodb
```

The YAML for a pod that will use persistent disk:
```
apiVersion: v1
kind: Pod
metadata:
  name: mongodb 
spec:
  volumes:
  - name: mongodb-data
    gcePersistentDisk:
      pdName: mongodb
      fsType: ext4
  containers:
  - image: mongo
    name: mongodb
    volumeMounts:
    - name: mongodb-data
      mountPath: /data/db
    ports:
    - containerPort: 27017
      protocol: TCP
```

Create the pod with disk attached and mounted:
```
kubectl apply -f mongodb-pod.yaml
```

See which node the pod landed on:
```
kubectl get pods -o wide
```

Connect to the mongodb shell:
```
kubectl exec -it mongodb mongo
```

Switch to the mystore database in the mongodb shell:
```
use mystore
```

Create a JSON document to insert into the database:
```
db.foo.insert({name:'foo'})
```

View the document you just created:
```
db.foo.find()
```

Exit from the mongodb shell:
```
exit
```

Delete the pod:
```
kubectl delete pod mongodb
```

Create a new pod with the same attached disk:
```
kubectl apply -f mongodb-pod.yaml
```

Check to see which node the pod landed on:
```
kubectl get pods -o wide
```

Drain the node (if the pod is on the same node as before):
```
kubectl drain [node_name] --ignore-daemonsets
```

Once the pod is on a different node, access the mongodb shell again:
```
kubectl exec -it mongodb mongo
```

Access the mystore database again:
```
use mystore
```

Find the document you created from before:
```
db.foo.find()
```

The YAML for a PersistentVolume object in Kubernetes:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mongodb-pv
spec:
  capacity: 
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
    - ReadOnlyMany
  persistentVolumeReclaimPolicy: Retain
  gcePersistentDisk:
    pdName: mongodb
    fsType: ext4
```

Create the Persistent Volume resource:
```
kubectl apply -f mongodb-persistentvolume.yaml
```

View our Persistent Volumes:
```
kubectl get persistentvolumes
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img49.png)

### Volume Access Modes
Volume access modes are how you specify the access of a node to your Persistent Volume. There are three types of access modes: ReadWriteOnce, ReadOnlyMany, and ReadWriteMany. In this lesson, we will explain what each of these access modes means and two VERY IMPORTANT things to remember when using your Persistent Volumes with pods.

![img](https://github.com/Bes0n/CKA/blob/master/images/img50.png)

The YAML for a Persistent Volume:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mongodb-pv
spec:
  capacity: 
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
    - ReadOnlyMany
  persistentVolumeReclaimPolicy: Retain
  gcePersistentDisk:
    pdName: mongodb
    fsType: ext4
```

View the Persistent Volumes in your cluster:
```
kubectl get pv
```

### Persistent Volume Claims
Persistent Volume Claims (PVCs) are a way for an application developer to request storage for the application without having to know where the underlying storage is. The claim is then bound to the Persistent Volume (PV), and it will not be released until the PVC is deleted. In this lesson, we will go through creating a PVC and accessing storage within our persistent disk.

![img](https://github.com/Bes0n/CKA/blob/master/images/img51.png)

The YAML for a PVC:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongodb-pvc 
spec:
  resources:
    requests:
      storage: 1Gi
  accessModes:
  - ReadWriteOnce
  storageClassName: ""
```

Create a PVC:
```
kubectl apply -f mongodb-pvc.yaml
```

View the PVC in the cluster:
```
kubectl get pvc
```

View the PV to ensure it’s bound:
```
kubectl get pv
```

The YAML for a pod that uses a PVC:
```
apiVersion: v1
kind: Pod
metadata:
  name: mongodb 
spec:
  containers:
  - image: mongo
    name: mongodb
    volumeMounts:
    - name: mongodb-data
      mountPath: /data/db
    ports:
    - containerPort: 27017
      protocol: TCP
  volumes:
  - name: mongodb-data
    persistentVolumeClaim:
      claimName: mongodb-pvc
```

Create the pod with the attached storage:
```
kubectl apply -f mongo-pvc-pod.yaml
```

Access the mongodb shell:
```
kubectl exec -it mongodb mongo
```

Find the JSON document created in previous lessons:
```
db.foo.find()
```

Delete the mongodb pod:
```
kubectl delete pod mogodb
```

Delete the mongodb-pvc PVC:
```
kubectl delete pvc mongodb-pvc
```

Check the status of the PV:
```
kubectl get pv
```

The YAML for the PV to show its reclaim policy:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mongodb-pv
spec:
  capacity: 
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
    - ReadOnlyMany
  persistentVolumeReclaimPolicy: Retain
  gcePersistentDisk:
    pdName: mongodb
    fsType: ext4
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img52.png)

### Storage Objects
There’s an even easier way to provision storage in Kubernetes with **StorageClass** objects. Also, your storage is safe from data loss with the “Storage Object in Use Protection” feature, which ensures any pods using a Persistent Volume will not lose the data on the volume as long as it is actively mounted. We’ve been using Google Storage for this section, but there are many different volume types you can use in Kubernetes. In this lesson, we will talk about the **hostPath** volume and the **empty** directory volume type.

![img](https://github.com/Bes0n/CKA/blob/master/images/img53.png)

See the PV protection on your volume:
```
kubectl describe pv mongodb-pv
```

See the PVC protection for your claim:
```
kubectl describe pvc mongodb-pvc
```

Delete the PVC:
```
kubectl delete pvc mongodb-pvc
```

See that the PVC is terminated, but the volume is still attached to pod:
```
kubectl get pvc
```

Try to access the data, even though we just deleted the PVC:
```
kubectl exec -it mongodb mongo
use mystore
db.foo.find()
```

Delete the pod, which finally deletes the PVC:
```
kubectl delete pods mongodb
```

Show that the PVC is deleted:
```
kubectl get pvc
```

YAML for a StorageClass object:
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-ssd
```

Create the StorageClass type "fast":
```
kubectl apply -f sc-fast.yaml
```

Change the PVC to include the new StorageClass object:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongodb-pvc 
spec:
  storageClassName: fast
  resources:
    requests:
      storage: 100Mi
  accessModes:
    - ReadWriteOnce
```

Create the PVC with automatically provisioned storage:
```
kubectl apply -f mongodb-pvc.yaml
```

View the PVC with new StorageClass:
```
kubectl get pvc
```


View the newly provisioned storage:
```
kubectl get pv
```


The YAML for a hostPath PV:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-hostpath
spec:
  storageClassName: local-storage
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

The YAML for a pod with an empty directory volume:
```
apiVersion: v1
kind: Pod
metadata:
  name: emptydir-pod
spec:
  containers:
  - image: busybox
    name: busybox
    command: ["/bin/sh", "-c", "while true; do sleep 3600; done"]
    volumeMounts:
    - mountPath: /tmp/storage
      name: vol
  volumes:
  - name: vol
    emptyDir: {}
```

Notes:
  - Even if you will delete your PVC, data still will be on POD, until POD removed. Once POD removed and get status *released* - pvc is going to be removed completely. 

![img](https://github.com/Bes0n/CKA/blob/master/images/img54.png)

### Applications with Persistent Storage
In this lesson, we’ll wrap everything up in a nice little bow and create a deployment that will allow us to use our storage with our pods. This is to demonstrate how a real-world application would be deployed and used for storing data.

![img](https://github.com/Bes0n/CKA/blob/master/images/img55.png)

In this lesson, we’ll wrap everything up in a nice little bow and create a deployment that will allow us to use our storage with our pods. This is to demonstrate how a real-world application would be deployed and used for storing data.

The YAML for our **StorageClass** object:
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-ssd
```

The YAML for our PVC:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: kubeserve-pvc 
spec:
  storageClassName: fast
  resources:
    requests:
      storage: 100Mi
  accessModes:
    - ReadWriteOnce
```

Create our StorageClass object:
```
kubectl apply -f storageclass-fast.yaml
```

View the StorageClass objects in your cluster:
```
kubectl get sc
```

Create our PVC:
```
kubectl apply -f kubeserve-pvc.yaml
```

View the PVC created in our cluster:
```
kubectl get pvc
```

View our automatically provisioned PV:
```
kubectl get pv
```

The YAML for our deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubeserve
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kubeserve
  template:
    metadata:
      name: kubeserve
      labels:
        app: kubeserve
    spec:
      containers:
      - env:
        - name: app
          value: "1"
        image: linuxacademycontent/kubeserve:v1
        name: app
        volumeMounts:
        - mountPath: /data
          name: volume-data
      volumes:
      - name: volume-data
        persistentVolumeClaim:
          claimName: kubeserve-pvc
```

Create our deployment and attach the storage to the pods:
```
kubectl apply -f kubeserve-deployment.yaml
```

Check the status of the rollout:
```
kubectl rollout status deployments kubeserve
```

Check the pods have been created:
```
kubectl get pods
```

Connect to our pod and create a file on the PV:
```
kubectl exec -it [pod-name] -- touch /data/file1.txt
```

Connect to our pod and list the contents of the /data directory:
```
kubectl exec -it [pod-name] -- ls /data
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img56.png)

### Creating Persistent Storage for Pods in Kubernetes
**Create a PersistentVolume.**
1. Use the following YAML spec for the PersistentVolume named redis-pv.yaml:
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: redis-pv
spec:
  storageClassName: ""
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

2. Then, create the PersistentVolume:
```
kubectl apply -f redis-pv.yaml
```

**Create a PersistentVolumeClaim.**
1. Use the following YAML spec for the PersistentVolumeClaim named redis-pvc.yaml:
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: redisdb-pvc
spec:
  storageClassName: ""
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

2. Then, create the PersistentVolumeClaim:
```
kubectl apply -f redis-pvc.yaml
```

**Create the redispod image, with a mounted volume to mount path** `/data`
1. Use the following YAML spec for the pod named redispod.yaml:
```
apiVersion: v1
kind: Pod
metadata:
  name: redispod
spec:
  containers:
  - image: redis
    name: redisdb
    volumeMounts:
    - name: redis-data
      mountPath: /data
    ports:
    - containerPort: 6379
      protocol: TCP
  volumes:
  - name: redis-data
    persistentVolumeClaim:
      claimName: redisdb-pvc
```

2. Then, create the pod:
```
kubectl apply -f redispod.yaml
```

3. Verify the pod was created:
```
kubectl get pods
```

**Connect to the container and write some data.**
1. Connect to the container and run the redis-cli:
```
kubectl exec -it redispod redis-cli
```

2. Set the key space server:name and value "redis server":
```
SET server:name "redis server"
```

3. Run the GET command to verify the value was set:
```
GET server:name
```
4. Exit the redis-cli:
```
QUIT
```

**Delete** `redispod` **and create a new pod named** `redispod2`.
1. Delete the existing redispod:
```
kubectl delete pod redispod
```

2. Open the file redispod.yaml and change line 4 from name: redispod to:
```
name: redispod2
```

3. Create a new pod named redispod2:
```
kubectl apply -f redispod.yaml
```

**Verify the volume has persistent data.**
1. Connect to the container and run redis-cli:
```
kubectl exec -it redispod2 redis-cli
```

2. Run the GET command to retrieve the data written previously:
```
GET server:name
```

3. Exit the redis-cli:
```
QUIT
```

## Securing the Kubernetes Cluster
### Kubernetes Security Primitives
Expanding on our discussion about securing the Kubernetes cluster, we’ll take a look at service accounts and user authentication. Also in this lesson, we will create a workstation for you to administer your cluster without logging in to the Kubernetes master server.

![img](https://github.com/Bes0n/CKA/blob/master/images/img57.png)

List the service accounts in your cluster:
```
kubectl get serviceaccounts
```

Create a new jenkins service account:
```
kubectl create serviceaccount jenkins
```

Use the abbreviated version of serviceAccount:
```
kubectl get sa
```

View the YAML for our service account:
```
kubectl get serviceaccounts jenkins -o yaml
```

View the secrets in your cluster:
```
kubectl get secret [secret_name]
```

The YAML for a busybox pod using the jenkins service account:
```
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  serviceAccountName: jenkins
  containers:
  - image: busybox:1.28.4
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
```

Create a new pod with the service account:
```
kubectl apply -f busybox.yaml
```

View the cluster config that kubectl uses:
```
kubectl config view
```

View the config file:
```
cat ~/.kube/config
```

Set new credentials for your cluster:
```
kubectl config set-credentials chad --username=chad --password=password
```

Create a role binding for anonymous users (not recommended):
```
kubectl create clusterrolebinding cluster-system-anonymous --clusterrole=cluster-admin --user=system:anonymous
```

SCP the certificate authority to your workstation or server:
```
scp ca.crt cloud_user@[pub-ip-of-remote-server]:~/
```

Set the cluster address and authentication:
```
kubectl config set-cluster kubernetes --server=https://172.31.41.61:6443 --certificate-authority=ca.crt --embed-certs=true
```

Set the credentials for Chad:
```
kubectl config set-credentials chad --username=chad --password=password
```

Set the context for the cluster:
```
kubectl config set-context kubernetes --cluster=kubernetes --user=chad --namespace=default
```

Use the context:
```
kubectl config use-context kubernetes
```

Run the same commands with kubectl:
```
kubectl get nodes
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img58.png)

### Cluster Authentication and Authorization
Once the API server has determined who you are (whether a pod or a user), the authorization is handled by RBAC. In this lesson, we will talk about roles, cluster roles, role bindings, and cluster role bindings.

![img](https://github.com/Bes0n/CKA/blob/master/images/img59.png)

Create a new namespace:
```
kubectl create ns web
```

The YAML for a service role:
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: web
  name: service-reader
rules:
- apiGroups: [""]
  verbs: ["get", "list"]
  resources: ["services"]
```

Create a new role from that YAML file:
```
kubectl apply -f role.yaml
```

Create a RoleBinding:
```
kubectl create rolebinding test --role=service-reader --serviceaccount=web:default -n web
```

Run a proxy for inter-cluster communications:
```
kubectl proxy
```

Try to access the services in the web namespace:
```
curl localhost:8001/api/v1/namespaces/web/services
```

Create a ClusterRole to access PersistentVolumes:
```
kubectl create clusterrole pv-reader --verb=get,list --resource=persistentvolumes
```

Create a ClusterRoleBinding for the cluster role:
```
kubectl create clusterrolebinding pv-test --clusterrole=pv-reader --serviceaccount=web:default
```

The YAML for a pod that includes a curl and proxy container:
```
apiVersion: v1
kind: Pod
metadata:
  name: curlpod
  namespace: web
spec:
  containers:
  - image: tutum/curl
    command: ["sleep", "9999999"]
    name: main
  - image: linuxacademycontent/kubectl-proxy
    name: proxy
  restartPolicy: Always
```

Create the pod that will allow you to curl directly from the container:
```
kubectl apply -f curl-pod.yaml
```

Get the pods in the web namespace:
```
kubectl get pods -n web
```

Open a shell to the container:
```
kubectl exec -it curlpod -n web -- sh
```

Access PersistentVolumes (cluster-level) from the pod:
```
curl localhost:8001/api/v1/persistentvolumes
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img60.png)

### Configuring Network Policies
Network policies allow you to specify which pods can talk to other pods. This helps when securing communication between pods, allowing you to identify ingress and egress rules. You can apply a network policy to a pod by using pod or namespace selectors. You can even choose a CIDR block range to apply the network policy. In this lesson, we’ll go through each of these options for network policies.

![img](https://github.com/Bes0n/CKA/blob/master/images/img61.png)

Download the canal plugin:
```
wget -O canal.yaml https://docs.projectcalico.org/v3.5/getting-started/kubernetes/installation/hosted/canal/canal.yaml
```

Apply the canal plugin:
```
kubectl apply -f canal.yaml
```

The YAML for a deny-all NetworkPolicy:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

Run a deployment to test the NetworkPolicy:
```
kubectl run nginx --image=nginx --replicas=2
```

Create a service for the deployment:
```
kubectl expose deployment nginx --port=80
```

Attempt to access the service by using a busybox interactive pod:
```
kubectl run busybox --rm -it --image=busybox /bin/sh
#wget --spider --timeout=1 nginx
```

The YAML for a pod selector NetworkPolicy:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-netpolicy
spec:
  podSelector:
    matchLabels:
      app: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: web
    ports:
    - port: 5432
```

Label a pod to get the NetworkPolicy:
```
kubectl label pods [pod_name] app=db
```

The YAML for a namespace NetworkPolicy:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ns-netpolicy
spec:
  podSelector:
    matchLabels:
      app: db
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          tenant: web
    ports:
    - port: 5432
```

The YAML for an IP block NetworkPolicy:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ipblock-netpolicy
spec:
  podSelector:
    matchLabels:
      app: db
  ingress:
  - from:
    - ipBlock:
        cidr: 192.168.1.0/24
```

The YAML for an egress NetworkPolicy:
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: egress-netpol
spec:
  podSelector:
    matchLabels:
      app: web
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: db
    ports:
    - port: 5432
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img62.png)

### Creating TLS Certificates
A Certificate Authority (CA) is used to generate TLS certificates and authenticate to your API server. In this lesson, we’ll go through certificate requests and generating a new certificate.

![img](https://github.com/Bes0n/CKA/blob/master/images/img63.png)

Find the CA certificate on a pod in your cluster:
```
kubectl exec busybox -- ls /var/run/secrets/kubernetes.io/serviceaccount
```

Download the binaries for the cfssl tool:
```
wget -q --show-progress --https-only --timestamping \
  https://pkg.cfssl.org/R1.2/cfssl_linux-amd64 \
  https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64
```

Make the binary files executable:
```
chmod +x cfssl_linux-amd64 cfssljson_linux-amd64
```

Move the files into your bin directory:
```
sudo mv cfssl_linux-amd64 /usr/local/bin/cfssl
sudo mv cfssljson_linux-amd64 /usr/local/bin/cfssljson
```

Check to see if you have cfssl installed correctly:
```
cfssl version
```

Create a CSR file:
```
cat <<EOF | cfssl genkey - | cfssljson -bare server
{
  "hosts": [
    "my-svc.my-namespace.svc.cluster.local",
    "my-pod.my-namespace.pod.cluster.local",
    "172.168.0.24",
    "10.0.34.2"
  ],
  "CN": "my-pod.my-namespace.pod.cluster.local",
  "key": {
    "algo": "ecdsa",
    "size": 256
  }
}
EOF
```

Create a CertificateSigningRequest API object:
```
cat <<EOF | kubectl create -f -
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  name: pod-csr.web
spec:
  groups:
  - system:authenticated
  request: $(cat server.csr | base64 | tr -d '\n')
  usages:
  - digital signature
  - key encipherment
  - server auth
EOF
```

View the CSRs in the cluster:
```
kubectl get csr
```

View additional details about the CSR:
```
kubectl describe csr pod-csr.web
```

Approve the CSR:
```
kubectl certificate approve pod-csr.web
```

View the certificate within your CSR:
```
kubectl get csr pod-csr.web -o yaml
```

Extract and decode your certificate to use in a file:
```
kubectl get csr pod-csr.web -o jsonpath='{.status.certificate}' \
    | base64 --decode > server.crt
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img64.png)

### Secure Images
Working with secure images is imperative in Kubernetes, as it ensures your applications are running efficiently and protecting you from vulnerabilities. In this lesson, we’ll go through how to set Kubernetes to use a private registry.

![img](https://github.com/Bes0n/CKA/blob/master/images/img65.png)

View where your Docker credentials are stored:
```
sudo vim /home/cloud_user/.docker/config.json
```

Log in to the Docker Hub:
```
sudo docker login
```

View the images currently on your server:
```
sudo docker images
```

Pull a new image to use with a Kubernetes pod:
```
sudo docker pull busybox:1.28.4
```

Log in to a private registry using the docker login command:
```
sudo docker login -u podofminerva -p 'otj701c9OucKZOCx5qrRblofcNRf3W+e' podofminerva.azurecr.io
```

View your stored credentials:
```
sudo vim /home/cloud_user/.docker/config.json
```

Tag an image in order to push it to a private registry:
```
sudo docker tag busybox:1.28.4 podofminerva.azurecr.io/busybox:latest
```

Push the image to your private registry:
```
docker push podofminerva.azurecr.io/busybox:latest
```

Create a new docker-registry secret:
```
kubectl create secret docker-registry acr --docker-server=https://podofminerva.azurecr.io --docker-username=podofminerva --docker-password='otj701c9OucKZOCx5qrRblofcNRf3W+e' --docker-email=user@example.com
```

Modify the default service account to use your new docker-registry secret:
```
kubectl patch sa default -p '{"imagePullSecrets": [{"name": "acr"}]}'
```

The YAML for a pod using an image from a private repository:
```
apiVersion: v1
kind: Pod
metadata:
  name: acr-pod
  labels:
    app: busybox
spec:
  containers:
    - name: busybox
      image: podofminerva.azurecr.io/busybox:latest
      command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
      imagePullPolicy: Always
```

Create the pod from the private image:
```
kubectl apply -f acr-pod.yaml
```

View the running pod:
```
kubectl get pods
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img66.png)

### Defining Security Contexts
Defining security contexts allows you to lock down your containers, so that only certain processes can do certain things. This ensures the stability of your containers and allows you to give control or take it away. In this lesson, we’ll go through how to set the security context at the container level and the pod level.

![img](https://github.com/Bes0n/CKA/blob/master/images/img67.png)

Run an alpine container with default security:
```
kubectl run pod-with-defaults --image alpine --restart Never -- /bin/sleep 999999
```

Check the ID on the container:
```
kubectl exec pod-with-defaults id
```

The YAML for a container that runs as a user:
```
apiVersion: v1
kind: Pod
metadata:
  name: alpine-user-context
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      runAsUser: 405
```

Create a pod that runs the container as user:
```
kubectl apply -f alpine-user-context.yaml
```

View the IDs of the new pod created with container user permission:
```
kubectl exec alpine-user-context id
```

The YAML for a pod that runs the container as non-root:
```
apiVersion: v1
kind: Pod
metadata:
  name: alpine-nonroot
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      runAsNonRoot: true
```

Create a pod that runs the container as non-root:
```
kubectl apply -f alpine-nonroot.yaml
```

View more information about the pod error:
```
kubectl describe pod alpine-nonroot
```

The YAML for a privileged container pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: privileged-pod
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      privileged: true
```

Create the privileged container pod:
```
kubectl apply -f privileged-pod.yaml
```

View the devices on the default container:
```
kubectl exec -it pod-with-defaults ls /dev
```

View the devices on the privileged pod container:
```
kubectl exec -it privileged-pod ls /dev
```

Try to change the time on a default container pod:
```
kubectl exec -it pod-with-defaults -- date +%T -s "12:00:00"
```

The YAML for a container that will allow you to change the time:
```
apiVersion: v1
kind: Pod
metadata:
  name: kernelchange-pod
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      capabilities:
        add:
        - SYS_TIME
```

Create the pod that will allow you to change the container’s time:
```
kubectl run -f kernelchange-pod.yaml
```

Change the time on a container:
```
kubectl exec -it kernelchange-pod -- date +%T -s "12:00:00"
```

View the date on the container:
```
kubectl exec -it kernelchange-pod -- date
```

The YAML for a container that removes capabilities:
```
apiVersion: v1
kind: Pod
metadata:
  name: remove-capabilities
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      capabilities:
        drop:
        - CHOWN
```

Create a pod that’s container has capabilities removed:
```
kubectl apply -f remove-capabilities.yaml
```

Try to change the ownership of a container with removed capability:
```
kubectl exec remove-capabilities chown guest /tmp
```

The YAML for a pod container that can’t write to the local filesystem:
```
apiVersion: v1
kind: Pod
metadata:
  name: readonly-pod
spec:
  containers:
  - name: main
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      readOnlyRootFilesystem: true
    volumeMounts:
    - name: my-volume
      mountPath: /volume
      readOnly: false
  volumes:
  - name: my-volume
    emptyDir:
```

Create a pod that will not allow you to write to the local container filesystem:
```
kubectl apply -f readonly-pod.yaml
```

Try to write to the container filesystem:
```
kubectl exec -it readonly-pod touch /new-file
```

Create a file on the volume mounted to the container:
```
kubectl exec -it readonly-pod touch /volume/newfile
```

View the file on the volume that’s mounted:
```
kubectl exec -it readonly-pod -- ls -la /volume/newfile
```

The YAML for a pod that has different group permissions for different pods:
```
apiVersion: v1
kind: Pod
metadata:
  name: group-context
spec:
  securityContext:
    fsGroup: 555
    supplementalGroups: [666, 777]
  containers:
  - name: first
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      runAsUser: 1111
    volumeMounts:
    - name: shared-volume
      mountPath: /volume
      readOnly: false
  - name: second
    image: alpine
    command: ["/bin/sleep", "999999"]
    securityContext:
      runAsUser: 2222
    volumeMounts:
    - name: shared-volume
      mountPath: /volume
      readOnly: false
  volumes:
  - name: shared-volume
    emptyDir:
```

Create a pod with two containers and different group permissions:
```
kubectl apply -f group-context.yaml
```

Open a shell to the first container on that pod:
```
kubectl exec -it group-context -c first sh
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img68.png)

### Securing Persistent Key Value Store
Secrets are used to secure sensitive data you may access from your pod. The data never gets written to disk because it's stored in an in-memory filesystem (tmpfs). Because secrets can be created independently of pods, there is less risk of the secret being exposed during the pod lifecycle.

![img](https://github.com/Bes0n/CKA/blob/master/images/img69.png)

View the secrets in your cluster:
```
kubectl get secrets
```

View the default secret mounted to each pod:
```
kubectl describe pods pod-with-defaults
```

View the token, certificate, and namespace within the secret:
```
kubectl describe secret
```

Generate a key for your https server:
```
openssl genrsa -out https.key 2048
```

Generate a certificate for the https server:
```
openssl req -new -x509 -key https.key -out https.cert -days 3650 -subj /CN=www.example.com
```

Create an empty file to create the secret:
```
touch file
```

Create a secret from your key, cert, and file:
```
kubectl create secret generic example-https --from-file=https.key --from-file=https.cert --from-file=file
```

View the YAML from your new secret:
```
kubectl get secrets example-https -o yaml
```

Create the configMap that will mount to your pod:
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: config
data:
  my-nginx-config.conf: |
    server {
        listen              80;
        listen              443 ssl;
        server_name         www.example.com;
        ssl_certificate     certs/https.cert;
        ssl_certificate_key certs/https.key;
        ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers         HIGH:!aNULL:!MD5;

        location / {
            root   /usr/share/nginx/html;
            index  index.html index.htm;
        }

    }
  sleep-interval: |
    25
```

The YAML for a pod using the new secret:
```
apiVersion: v1
kind: Pod
metadata:
  name: example-https
spec:
  containers:
  - image: linuxacademycontent/fortune
    name: html-web
    env:
    - name: INTERVAL
      valueFrom:
        configMapKeyRef:
          name: config
          key: sleep-interval
    volumeMounts:
    - name: html
      mountPath: /var/htdocs
  - image: nginx:alpine
    name: web-server
    volumeMounts:
    - name: html
      mountPath: /usr/share/nginx/html
      readOnly: true
    - name: config
      mountPath: /etc/nginx/conf.d
      readOnly: true
    - name: certs
      mountPath: /etc/nginx/certs/
      readOnly: true
    ports:
    - containerPort: 80
    - containerPort: 443
  volumes:
  - name: html
    emptyDir: {}
  - name: config
    configMap:
      name: config
      items:
      - key: my-nginx-config.conf
        path: https.conf
  - name: certs
    secret:
      secretName: example-https
```

Apply the config map and the example-https yaml files:
```
kubectl apply -f configmap.yaml
kubectl apply -f example-https.yaml
```

Describe the nginx conf via ConfigMap:
```
kubectl describe configmap
```

View the cert mounted on the container:
```
kubectl exec example-https -c web-server -- mount | grep certs
```

Use port forwarding on the pod to server traffic from 443:
```
kubectl port-forward example-https 8443:443 &
```

Curl the web server to get a response:
```
curl https://localhost:8443 -k
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img70.png)

### Creating a ClusterRole to Access a PV in Kubernetes
**View the Persistent Volume.**
- Use the following command to view the Persistent Volume within the cluster:
```
kubectl get pv
```

**Create a ClusterRole.**
- Use the following command to create the ClusterRole:
```
kubectl create clusterrole pv-reader --verb=get,list --resource=persistentvolumes 
```

**Create a ClusterRoleBinding.**
- Use the following command to create the ClusterRoleBinding:
```
kubectl create clusterrolebinding pv-test --clusterrole=pv-reader --serviceaccount=web:default
```

**Create a pod to access the PV.**
1. Use the following YAML to create a pod that will proxy the connection and allow you to curl the address:
```
 apiVersion: v1
 kind: Pod
 metadata:
   name: curlpod
   namespace: web
 spec:
   containers:
   - image: tutum/curl
     command: ["sleep", "9999999"]
     name: main
   - image: linuxacademycontent/kubectl-proxy
     name: proxy
   restartPolicy: Always
```

2. Use the following command to create the pod:
```
 kubectl apply -f curlpod.yaml
```

**Request access to the PV from the pod.**
1. Use the following command (from within the pod) to access a shell from the pod:
```
 kubectl exec -it curlpod -n web -- sh
```

2. Use the following command to curl the PV resource:
```
 curl localhost:8001/api/v1/persistentvolumes
```

## Monitoring Cluster Components
### Monitoring the Cluster Components
We are able to monitor the CPU and memory utilization of our pods and nodes by using the metrics server. In this lesson, we’ll install the metrics server and see how the kubectl top command works.

![img](https://github.com/Bes0n/CKA/blob/master/images/img71.png)

Clone the metrics server repository:
```
git clone https://github.com/linuxacademy/metrics-server
```

Install the metrics server in your cluster:
```
kubectl apply -f ~/metrics-server/deploy/1.8+/
```

Get a response from the metrics server API:
```
kubectl get --raw /apis/metrics.k8s.io/
```

Get the CPU and memory utilization of the nodes in your cluster:
```
kubectl top node
```

Get the CPU and memory utilization of the pods in your cluster:
```
kubectl top pods
```

Get the CPU and memory of pods in all namespaces:
```
kubectl top pods --all-namespaces
```

Get the CPU and memory of pods in only one namespace:
```
kubectl top pods -n kube-system
```

Get the CPU and memory of pods with a label selector:
```
kubectl top pod -l run=pod-with-defaults
```

Get the CPU and memory of a specific pod:
```
kubectl top pod pod-with-defaults
```

Get the CPU and memory of the containers inside the pod:
```
kubectl top pods group-context --containers
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img72.png)

### Monitoring the Applications Running within a Cluster
There are ways Kubernetes can automatically monitor your apps for you and, furthermore, fix them by either restarting or preventing them from affecting the rest of your service. You can insert liveness probes and readiness probes to do just this for custom monitoring of your applications.

![img](https://github.com/Bes0n/CKA/blob/master/images/img73.png)

The pod YAML for a liveness probe:
```
apiVersion: v1
kind: Pod
metadata:
  name: liveness
spec:
  containers:
  - image: linuxacademycontent/kubeserve
    name: kubeserve
    livenessProbe:
      httpGet:
        path: /
        port: 80
```

The YAML for a service and two pods with readiness probes:
```
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: nginx
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
---
apiVersion: v1
kind: Pod
metadata:
  name: nginxpd
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:191
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 5
```

Create the service and two pods with readiness probes:
```
kubectl apply -f readiness.yaml
```

Check if the readiness check passed or failed:
```
kubectl get pods
```

Check if the failed pod has been added to the list of endpoints:
```
kubectl get ep
```

Edit the pod to fix the problem and enter it back into the service:
```
kubectl edit pod [pod_name]
```

Get the list of endpoints to see that the repaired pod is part of the service again:
```
kubectl get ep
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img74.png)

### Managing Cluster Component Logs
There are many ways to manage the logs that can accumulate from both applications and system components. In this lesson, we’ll go through a few different approaches to organizing your logs.

![img](https://github.com/Bes0n/CKA/blob/master/images/img75.png)

The directory where the container logs reside:
```
/var/log/containers
```

The directory where kubelet stores its logs:
```
/var/log
```

The YAML for a pod that has two different log streams:
```
apiVersion: v1
kind: Pod
metadata:
  name: counter
spec:
  containers:
  - name: count
    image: busybox
    args:
    - /bin/sh
    - -c
    - >
      i=0;
      while true;
      do
        echo "$i: $(date)" >> /var/log/1.log;
        echo "$(date) INFO $i" >> /var/log/2.log;
        i=$((i+1));
        sleep 1;
      done
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  volumes:
  - name: varlog
    emptyDir: {}
```

Create a pod that has two different log streams to the same directory:
```
kubectl apply -f twolog.yaml
```

View the logs in the /var/log directory of the container:
```
kubectl exec counter -- ls /var/log
```

The YAML for a sidecar container that will tail the logs for each type:
```
apiVersion: v1
kind: Pod
metadata:
  name: counter
spec:
  containers:
  - name: count
    image: busybox
    args:
    - /bin/sh
    - -c
    - >
      i=0;
      while true;
      do
        echo "$i: $(date)" >> /var/log/1.log;
        echo "$(date) INFO $i" >> /var/log/2.log;
        i=$((i+1));
        sleep 1;
      done
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  - name: count-log-1
    image: busybox
    args: [/bin/sh, -c, 'tail -n+1 -f /var/log/1.log']
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  - name: count-log-2
    image: busybox
    args: [/bin/sh, -c, 'tail -n+1 -f /var/log/2.log']
    volumeMounts:
    - name: varlog
      mountPath: /var/log
  volumes:
  - name: varlog
    emptyDir: {}
```

View the first type of logs separately:
```
kubectl logs counter count-log-1
```

View the second type of logs separately:
```
kubectl logs counter count-log-2
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img76.png)

### Managing Application Logs
Containerized applications usually write their logs to standard out and standard error instead of writing their logs to files. Docker then redirects those streams to files. You can retrieve those files with the kubectl logs command in Kubernetes. In this lesson, we’ll go over the many ways to manipulate the output of your logs and redirect them to a file.

![img](https://github.com/Bes0n/CKA/blob/master/images/img77.png)

Get the logs from a pod:
```
kubectl logs nginx
```

Get the logs from a specific container on a pod:
```
kubectl logs counter -c count-log-1
```

Get the logs from all containers on the pod:
```
kubectl logs counter --all-containers=true
```

Get the logs from containers with a certain label:
```
kubectl logs -lapp=nginx
```

Get the logs from a previously terminated container within a pod:
```
kubectl logs -p -c nginx nginx
```

Stream the logs from a container in a pod:
```
kubectl logs -f -c count-log-1 counter
```

Tail the logs to only view a certain number of lines:
```
kubectl logs --tail=20 nginx
```

View the logs from a previous time duration:
```
kubectl logs --since=1h nginx
```

View the logs from a container within a pod within a deployment:
```
kubectl logs deployment/nginx -c nginx
```

Redirect the output of the logs to a file:
```
kubectl logs counter -c count-log-1 > count.log
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img78.png)

### Monitor and Output Logs to a File in Kubernetes

**Identify the problematic pod in your cluster.**
- Use the following command to view all the pods in your cluster:
```
kubectl get pods --all-namespaces
```

**Collect the logs from the pod.**
- Use the following command to collect the logs from the pod:
```
kubectl logs <pod_name> -n <namespace_name>
```

**Output the logs to a file.**
- Use the following command to output the logs to a file:
```
kubectl logs <pod_name> -n <namespace_name> > broken-pod.log
```

## Identifying Failure within the Kubernetes Cluster
### Troubleshooting Application Failure
Application failure can happen for many reasons, but there are ways within Kubernetes that make it a little easier to discover why. In this lesson, we’ll fix some broken pods and show common methods to troubleshoot.

![img](https://github.com/Bes0n/CKA/blob/master/images/img79.png)

The YAML for a pod with a termination reason:
```
apiVersion: v1
kind: Pod
metadata:
  name: pod2
spec:
  containers:
  - image: busybox
    name: main
    command:
    - sh
    - -c
    - 'echo "I''ve had enough" > /var/termination-reason ; exit 1'
    terminationMessagePath: /var/termination-reason
```

One of the first steps in troubleshooting is usually to describe the pod:
```
kubectl describe po pod2
```

The YAML for a liveness probe that checks for pod health:
```
apiVersion: v1
kind: Pod
metadata:
  name: liveness
spec:
  containers:
  - image: linuxacademycontent/candy-service:2
    name: kubeserve
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8081
```

View the logs for additional detail:
```
kubectl logs pod-with-defaults
```

Export the YAML of a running pod, in the case that you are unable to edit it directly:
```
kubectl get po pod-with-defaults -o yaml --export > defaults-pod.yaml
```

Edit a pod directly (i.e., changing the image):
```
kubectl edit po nginx
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img80.png)

### Troubleshooting Control Plane Failure
The Kubernetes Control Plane is an important component to back up and protect against failure. There are certain best practices you can take to ensure you don’t have a single point of failure. If your Control Plane components are not effectively communicating, there are a few things you can check to ensure your cluster is operating efficiently.

![img](https://github.com/Bes0n/CKA/blob/master/images/img81.png)

Check the events in the **kube-system** namespace for errors:
```
kubectl get events -n kube-system
```

Get the logs from the individual pods in your **kube-system** namespace and check for errors:
```
kubectl logs [kube_scheduler_pod_name] -n kube-system
```

Check the status of the Docker service:
```
sudo systemctl status docker
```

Start up and enable the Docker service, so it starts upon bootup:
```
sudo systemctl enable docker && systemctl start docker
```

Check the status of the kubelet service:
```
sudo systemctl status kubelet
```

Start up and enable the kubelet service, so it starts up when the machine is rebooted:
```
sudo systemctl enable kubelet && systemctl start kubelet
```

Turn off swap on your machine:
```
sudo su -
swapoff -a && sed -i '/ swap / s/^/#/' /etc/fstab
```

Check if you have a firewall running:
```
sudo systemctl status firewalld
```

Disable the firewall and stop the firewalld service:
```
sudo systemctl disable firewalld && systemctl stop firewalld
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img82.png)

### Troubleshooting Worker Node Failure
Troubleshooting worker node failure is a lot like troubleshooting a non-responsive server, in addition to the kubectl tools we have at our disposal. In this lesson, we’ll learn how to recover a node and add it back to the cluster and find out how to identify when the kublet service is down.

![img](https://github.com/Bes0n/CKA/blob/master/images/img83.png)

Listing the status of the nodes should be the first step:
```
kubectl get nodes
```

Find out more information about the nodes with kubectl describe:
```
kubectl describe nodes chadcrowell2c.mylabserver.com
```

You can try to log in to your server via SSH:
```
ssh chadcrowell2c.mylabserver.com
```

Get the IP address of your nodes:
```
kubectl get nodes -o wide
```

Use the IP address to further probe the server:
```
ssh cloud_user@172.31.29.182
```

Generate a new token after spinning up a new server:
```
sudo kubeadm token generate
```

Create the kubeadm join command for your new worker node:
```
sudo kubeadm token create [token_name] --ttl 2h --print-join-command
```

View the journalctl logs:
```
sudo journalctl -u kubelet
```

View the syslogs:
```
sudo more syslog | tail -120 | grep kubelet
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img84.png)

### Troubleshooting Networking
Network issues usually start to arise internally or when using a service. In this lesson, we’ll go through the many methods to see if your app is serving traffic by creating a service and testing the communication within the cluster.

![img](https://github.com/Bes0n/CKA/blob/master/images/img85.png)

Run a deployment using the container port 9376 and with three replicas:
```
kubectl run hostnames --image=k8s.gcr.io/serve_hostname \
                        --labels=app=hostnames \
                        --port=9376 \
                        --replicas=3
```

List the services in your cluster:
```
kubectl get svc
```

Create a service by exposing a port on the deployment:
```
kubectl expose deployment hostnames --port=80 --target-port=9376
```

Run an interactive busybox pod:
```
kubectl run -it --rm --restart=Never busybox --image=busybox:1.28 sh
```

From the pod, check if DNS is resolving hostnames:
```
# nslookup hostnames
```

From the pod, cat out the /etc/resolv.conf file:
```
# cat /etc/resolv.conf
```

From the pod, look up the DNS name of the Kubernetes service:
```
# nslookup kubernetes.default
```

Get the JSON output of your service:
```
kubectl get svc hostnames -o json
```

View the endpoints for your service:
```
kubectl get ep
```

Communicate with the pod directly (without the service):
```
wget -qO- 10.244.1.6:9376
```

Check if kube-proxy is running on the nodes:
```
ps auxw | grep kube-proxy
```

Check if kube-proxy is writing iptables:
```
iptables-save | grep hostnames
```

View the list of kube-system pods:
```
kubectl get pods -n kube-system
```

Connect to your kube-proxy pod in the kube-system namespace:
```
kubectl exec -it kube-proxy-cqptg -n kube-system -- sh
```

Delete the flannel CNI plugin:
```
kubectl delete -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml
```

Apply the Weave Net CNI plugin:
```
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

![img](https://github.com/Bes0n/CKA/blob/master/images/img86.png)

### Repairing Failed Pods in Kubernetes
**Identify the broken pods.**
- Use the following command to see what’s in the cluster:
```
kubectl get all --all-namespaces
```

**Find out why the pods are broken.**
- Use the following command to inspect the pod and view the events:
```
kubectl describe pod <pod_name>
```

**Repair the broken pods.**
1. Use the following command to repair the broken pods in the most efficient manner:
```
 kubectl edit deploy nginx -n web
```

2. Where it says image: **nginx:191**, change it to **image: nginx**. Save and exit.

3. Verify the repair is complete:
```
 kubectl get po -n web
```

4. See the new replica set:
```
 kubectl get rs -n web
```

**Ensure pod health by accessing the pod directly.**
1. List the pods including the IP addresses:
```
 kubectl get po -n web -o wide
```

2. Start a busybox pod:
```
 kubectl run busybox --image=busybox --rm -it --restart=Never -- sh
```

3. Use the following command to access the pod directly via its container port, replacing POD_IP_ADDRESS with an appropriate pod IP:
```
 wget -qO- POD_IP_ADDRESS:80
```

## Hands-On Practice Exam
### CKA Practice Exam: Part 1
##### Additional Information and Resources
You have been given access to a three-node cluster. Within that cluster, you will be responsible for creating a service for end users of your web application. You will ensure the application meets the specifications set by the developers and the proper resources are in place to ensure maximum uptime for the app. You must perform the following tasks in order to complete this hands-on lab:

- All objects should be in the `web` namespace.
- The deployment name should be `webapp`.
- The deployment should have 3 replicas.
- The deployment’s pods should have one container using the `linuxacademycontent/podofminerva` image with the tag `latest`.
- The service should be named `web-service`.
- The service should forward traffic to port 80 on the pods.
- The service should be exposed externally by listening on port 30080 on each node.
- The pods should be configured to check the `/healthz`. endpoint on port 8081, and automatically restart the container if the check fails.
- The pods should be configured to not receive traffic until the endpoint on port 80 responds successfully.

**Create a deployment named `webapp` in the `web` namespace and verify connectivity.**
1. Use the following command to create a namespace named `web`:
```
 kubectl create ns web
```

2. Use the following command to create a deployment named webapp:
```
kubectl run webapp --image=linuxacademycontent/podofminerva:latest --port=80 --replicas=3 -n web
```
**Create a service named `web-service` and forward traffic from the pods.**
1. Use the following command to get the IP address of a pod that’s a part of the deployment:
```
kubectl get po -o wide -n web
```

2. Use the following command to create a temporary pod with a shell to its container:
```
 kubectl run busybox --image=busybox --rm -it --restart=Never -- sh
```

3. Use the following command (from the container’s shell) to send a request to the web pod:
```
 wget -O- <pod_ip_address>:80
```

4. Use the following command to create the YAML for the service named `web-service`:
```
 kubectl expose deployment/webapp --port=80 --target-port=80 --type=NodePort -n web --dry-run -o yaml > web-service.yaml
```

5. Use Vim to add the namespace and the NodePort to the YAML:
```
vim web-service.yaml
```
  
Change the name to `web-service`, add the namespace `web`, and add nodePort: 30080.

6. Use the following command to create the service:
```
 kubectl apply -f web-service.yaml
```

7. Use the following command to verify that the service is responding on the correct port:
```
 curl localhost:30080
```

8. Use the following command to modify the deployment:
```
 kubectl edit deploy webapp -n web
```

9. Add the liveness probe and the readiness probe::
```
 livenessProbe:
   httpGet:
     path: /healthz
     port: 8081
 readinessProbe:
   httpGet:
     path: /
     port: 80
```

10. Use the following command to check if the pods are running:
```
kubectl get po -n web
```

11. Use the following command to check if the probes were added to the pods:
```
 kubectl get po <pod_name> -o yaml -n web --export
```

### CKA Practice Exam: Part 2
##### Additional Information and Resources
You have been given access to a two-node cluster. Within that cluster, a `PersistentVolume` has already been created. You must identify the size of the volume in order to make a `PersistentVolumeClaim` and mount the volume to your pod. Once you have created the PVC and mounted it to your running pod, you must copy the contents of `/etc/passwd` to the volume. Finally, you will delete the pod and create a new pod with the volume mounted in order to demonstrate the persistence of data. You must perform the following tasks in order to complete this hands-on lab:

- All objects should be in the `web` namespace.
- The `PersistentVolumeClaim` name should be `data-pvc`.
- The PVC request should be 256 MiB.
- The access mode for the PVC should be `ReadWriteOnce`.
- The storage class name should be local-storage.
- The pod name should be `data-pod`.
- The pod image should be `busybox` and the tag should be `1.28`.
- The pod should request the `PersistentVolumeClaim` named `data-pvc`, and the volume name should be temp-data.
- The pod should mount the volume named `temp-data` to the `/tmp/data` directory.
- The name of the second pod should be `data-pod2`.

**Create the `PersistentVolumeClaim`.**
1. Use the following command to check if there is already a `web` namespace:
```
kbuectl get ns
```

2. Use the following command to create a `PersistentVolumeClaim`:
```
vi data-pvc.yaml #copy and paste from docs
```

3. Change the following in the `data-pvc.yaml` file:
```
name: data-pvc
namespace: web
storageClassName: local-storage
storage: 256Mi
```

4. Use the following command to create the PVC:
```
kubectl apply -f data-pvc.yaml
```

**Create a pod mounting the volume and write data to the volume.**
1. Use the following command to create the YAML for a busybox pod:
```
kubectl run data-pod --image=busybox --restart=Never -o yaml --dry-run -- /bin/sh -c 'sleep 3600' > data-pod.yaml
```

2. Use the following command to edit the `data-pod.yaml` file:
```
vi data-pod.yaml
```

3. Add the following to the `data-pod.yaml` file:
```
apiVersion: v1
kind: Pod
metadata:
  name: data-pod
  namespace: web
spec:
  containers:
  - args:
    - /bin/sh
    - -c
    - sleep 3600
    image: busybox:1.28
    name: data-pod
    resources: {}
    volumeMounts: 
    - name: temp-data
      mountPath: /tmp/data
  dnsPolicy: ClusterFirst
  restartPolicy: Never
  volumes: 
  - name: temp-data
    persistentVolumeClaim:
      claimName: data-pvc
```

4. Use the following command to create the pod:
```
kubectl apply -f data-pod.yaml
```

5. Use the following command to connect to the pod:
```
kubectl exec -it data-pod -n web -- sh
```

6. Use the following command to copy the contents of the `etc/passwd` file to `/tmp/data`:
```
# cp /etc/passwd /tmp/data/passwd
```

7. Use the following command to list the contents of `/tmp/data`:
```
# ls /tmp/data/
```

**Delete the pod and create a new pod and view volume data.**
1. Use the following command to delete the pod:
```
 kubectl delete po data-pod -n web
```

2. Use the following command to modify the pod YAML:
```
vi data-pod.yaml
```

3. Change the following line in the `data-pod.yaml` file:
```
name: data-pod2
```

4. Use the following command to create a new pod:
```
 kubectl apply -f data-pod.yaml
```

5. Use the following command to connect to the pod and view the contents of the volume:
```
 kubectl exec -it data-pod2 -n web -- sh
 # ls /tmp/data
```

### CKA Practice Exam: Part 3
##### Additional Information and Resources
You have been given access to a three-node cluster. You will be responsible for creating a deployment and a service to serve as a front end for a web application. In addition to the web application, you must deploy a Redis database and make sure the web application can only access this database using the default port of 6379. You will first create a `default-deny` network policy, so all pods within your Kubernetes are not able to communicate with each other by default. Then you will create a second network policy that specifies the communication on port 6379 between the web application and the database using their label selectors. You must apply these specifications to your resources in order to complete this hands-on lab:

- Create a deployment named `webfront-deploy`.
- The deployment should use the image `nginx` with the tag `1.7.8`.
- The deployment should expose container port 80 on each pod and contain 2 replicas.
- Create a service named `webfront-service` and expose port 80, target port 80.
- The service should be exposed externally by listening on port 30080 on each node.
- Create one pod named `db-redis` using the image `redis` and the tag `latest`.
- Verify that you can communicate to pods by default.
- Create a network policy named `default-deny` that will deny pod communication by default.
- Verify that you can no longer communicate between pods.
- Apply the label `role=frontend` to the web application pods and the label `role=db` to the database pod.
- Create a network policy that will apply an ingress rule for the pods labeled with `role=db` to allow traffic on port 6379 from the pods labeled - `role=frontend`.
- Verify that you have applied the correct labels and created the correct network policies.

**Create a deployment and a service to expose your web front end.**
1. Use the following command to create the YAML for your deployment:
```
kubectl create deployment webfront-deploy  --image=nginx:1.7.8  --dry-run -o yaml > webfront-deploy.yaml
```

2. Add container port 80, to have your final YAML look like this:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: webfront-deploy
  name: webfront-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: webfront-deploy
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: webfront-deploy
    spec:
      containers:
      - image: nginx:1.7.8
        name: nginx
        resources: {}
        ports:
        - containerPort: 80
status: {}
```

3. Use the following command to create your deployment:
```
kubectl apply -f webfront-deploy.yaml
```

4. Use the following command to scale up your deployment:
```
kubectl scale deployment/webfront-deploy --replicas=2
```

5. Use the following command to create the YAML for a service:
```
kubectl expose deployment/webfront-deploy --port=80 --target-port=80 --type=NodePort --dry-run -o yaml > webfront-service.yaml
```

6. Add the name and the nodePort, the complete YAML will look like this:
```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: webfront-deploy
  name: webfront-service
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 30080
  selector:
    app: webfront-deploy
  type: NodePort
status:
  loadBalancer: {}
```

7. Use the following command to create the service:
```
kubectl apply -f webfront-service.yaml
```

8. Verify that you can communicate with your pod directly:
```
kubectl run busybox --rm -it --image=busybox /bin/sh

# wget -O- <pod_ip_address>:80
# wget --spider --timeout=1 webfront-service
```

**Create a database server to serve as the backend database.**
- Use the following command to create a Redis pod:
```
kubectl run db-redis --image=redis --restart=Never
```

**Create a network policy that will deny communication by default.**
1. Use the following YAML (this is where you can use kubernetes.io and search "network policies" and then search for the text "default"):

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
spec:
  podSelector: {}
  policyTypes:
  - Ingress
```

2. Use the following command to apply the network policy:
```
kubectl apply -f default-deny.yaml
```

3. Verify that communication has been disabled by default:
```
kubectl run busybox --rm -it --image=busybox /bin/sh
# wget -O- ≤pod_ip_address>:80
```

**Apply the labels and create a communication over port 6379 to the database server.**
1. Use the following commands to apply the labels:
```
kubectl get po
kubectl label po <pod_name> role=frontend
kubectl label po db-redis role=db
kubectl get po --show-labels
```

2. Use the following YAML to create a network policy for the communication between the two labeled pods (copy from kubernetes.io website):

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: redis-netpolicy
spec:
  podSelector:
    matchLabels:
      role: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - port: 6379
```

3. Use the following command to create the network policy:
```
kubectl apply -f redis-netpolicy.yaml
```

4. Use the following command to view the network policies:
```
kubectl get netpol
```

5. Use the following command to describe the custom network policy:
```
kubectl describe netpol redis-netpolicy
```

6. Use the following command to show the labels on the pods:
```
kubectl get po --show-labels
```