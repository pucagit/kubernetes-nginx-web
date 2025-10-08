# Kubernetes
## What can Kubernetes do for you?
With modern web services, users expect applications to be available 24/7, and developers expect to deploy new versions of those applications several times a day. Containerization helps package software to serve these goals, enabling applications to be released and updated without downtime. Kubernetes helps you make sure those containerized applications run where and when you want, and helps them find the resources and tools they need to work. 

Kubernetes provides you with:
- **Service discovery and load balancing** Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
- **Storage orchestration** Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.
- **Automated rollouts and rollbacks** You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.
- **Automatic bin packing** You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.
- **Self-healing** Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.
- **Secret and configuration management** Kubernetes lets you store and manage sensitive information, such as passwords, OAuth tokens, and SSH keys. You can deploy and update secrets and application configuration without rebuilding your container images, and without exposing secrets in your stack configuration.
- **Batch execution** In addition to services, Kubernetes can manage your batch and CI workloads, replacing containers that fail, if desired.
- **Horizontal scaling** Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.
- **IPv4/IPv6 dual-stack** Allocation of IPv4 and IPv6 addresses to Pods and Services
- **Designed for extensibility** Add features to your Kubernetes cluster without changing upstream source code.


## Kubernetes Clusters
Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit. 
Kubernetes automates the distribution and scheduling of application containers across a cluster in a more efficient way.
A Kubernetes cluster consists of two types of resources:
- The **Control Plane** coordinates the cluster (responsible for managing the cluster, e.g. scheduling applications, maintaining application's desired state, scaling applications, rolling out new updates)
- **Node** is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster. Each node has a Kubelet, which is an agent for managing the node and communicating with the Kubernetes control plane.

**Minikube** is a lightweight Kubernetes implementation that creates a VM on your local machine and deploys a simple cluster containing only one node. 

## Kubernetes Components
![alt text](k8scomps.png)
### Core Components
**Control Plane Components**
- **kube-apiserver**: The core component server that exposes the Kubernetes HTTP API.
- **kube-scheduler**: Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node.
- **kube-controller-manager**: Runs controllers to implement Kubernetes API behavior.
- **cloud-controller-manager** (optional): Integrates with underlying cloud provider(s).
- **etcd**: Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.
  
**Node Components**
- **kubelet**: Ensures that Pods are running, including their containers, ensures that the containers described in PodSpecs are running and healthy.
- **kube-proxy** (optional): Maintains network rules on nodes to implement Services (works like a load balancer)
- **Container runtime**: Software responsible for running containers (manage the execution and lifecycle of containers within the Kubernetes environment.)

**DNS**: Cluster DNS is a DNS server, in addition to the other DNS server(s) in your environment, which serves DNS records for Kubernetes services. Containers started by Kubernetes automatically include this DNS server in their DNS searches.

## The Kubernetes API
The Kubernetes API lets you query and manipulate the state of objects in Kubernetes. The core of Kubernetes' control plane is the API server and the HTTP API that it exposes. Users, the different parts of your cluster, and external components all communicate with one another through the API server.
- **Discovery API**: provides information about the Kubernetes APIs: API names, resources, versions, and supported operations.
- **OpenAPI v2.0 and OpenAPI v3.0**: includes all the available API paths, as well as all resources consumed and produced for every operations on every endpoints. It also includes any extensibility components that a cluster supports. The data is a complete specification and is significantly larger than that from the Discovery API.

## Communication between Nodes and the Control Plane
**Node to Control Plane**: Kubernetes has a "hub-and-spoke" API pattern. All API usage from nodes (or the pods they run) terminates at the API server. None of the other control plane components are designed to expose remote services. The API server is configured to listen for remote connections on a secure HTTPS port (typically 443) with one or more forms of client authentication enabled. One or more forms of authorization should be enabled, especially if anonymous requests or service account tokens are allowed.

**Control plane to node**: There are two primary communication paths from the control plane (the API server) to the nodes:
- **API server to kubelet**: used for fetching logs for pods, attaching to running pods, providing the kubelet's port-forwarding functionality. (By default, the API server does not verify the kubelet's serving certificate, which makes the connection subject to man-in-the-middle attacks and unsafe to run over untrusted and/or public networks.)
- **API server to nodes, pods, and services**: default to plain HTTP connections and are therefore neither authenticated nor encrypted.
- **SSH tunnels**: the API server initiates an SSH tunnel to each node in the cluster (connecting to the SSH server listening on port 22) and passes all traffic destined for a kubelet, node, pod, or service through the tunnel.
- **Konnectivity service**: a replacement to the SSH tunnels, provides TCP level proxy for the control plane to cluster communication.

## Kubernetes definitions
**Pod**
- Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
- A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.
- Every Pod has a unique IP address, this IP is reachable from all other Pods in the K8s cluster.

**Service**
- Service is a method for exposing a network application that is running as one or more Pods in your cluster.
- Each Pod gets its own IP address and they could change. Service serves as a load balancer for these groups of Pods with its own stable IP.
- Service types:
    - `ClusterIP` (default): Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service.
  ![alt text](clusterip.png)
    - `NodePort`: Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: `ClusterIP`.
  ![alt text](nodeport.png)
    - `LoadBalancer`: Open a node port only accessible through the Load Balancer.
  ![alt text](loadbalancer.png)
    - `ExternalName`: Maps the Service to the contents of the `externalName` field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. No proxying of any kind is set up.
  
**Ingress**
- Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster.

**Ingress Controller**
- evaluates all the rules inside nginx
- manages redirections
- entrypoint to cluster
- **Flow:** External load balancer receives request → Forwards it to Ingress Controller → Ingress Controller applies Ingress rules → Traffic is redirected to internal Service → Pod

**ConfigMap**
- External Configuration of your application
- Like mounting volumes in Docker (but only for configs - small text files)

**Secret**
- Used to store secret data (not encrpyted, must use 3rd party tools to encrypt secrets)
- Reference Secret in Deployment/Pod

**Volume**
- Storage on local machine or remote, outside of the K8s cluster
- Attach to Pod's storage

**Deployment**
- A Deployment manages a set of Pods to run an application workload, usually one that doesn't maintain state.
- Replicate Pods as distributed system so that if one 1 Pod dies, the Service could route to the replica.
- Supports version controll (roll out and roll back changes)

**Statefulset**
- For stateful apps like databases (DBs are often hosted outside K8s clusters)
- Like Deployment

## Kubernetes Network
**Container Communication**


## Kubernetes Flow
![alt text](KubectlFlow.png)

## View resource usage
The Metrics Server is a crucial component for collecting and serving resource usage metrics (CPU and memory) from nodes and pods, which `kubectl top` relies on. If the Metrics Server is missing, you need to deploy it. You can typically find the manifest files in the official Kubernetes Metrics Server GitHub repository.
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
Running this command applies the metrics server configuration YAML in the given URL and installs it in your cluster. After this, you can verify its status:
```
kubectl get deployment metrics-server -n kube-system
```
We see that even though it was deployed a while ago, metrics-server still hasn’t been up yet. We can check its logs with:
```
kubectl logs deployment/metrics-server -n kube-system
```
Here, the important thing is the error:
```
E0306 17:19:41.746695       1 scraper.go:149] "Failed to scrape node" err="Get \"https://192.168.49.2:10250/metrics/resource\": tls: failed to verify certificate: x509: cannot validate certificate for 192.168.49.2 because it doesn't contain any IP SANs" node="minikube"
```
We need to add the config `serverTLSBootstrap: true` to the ConfigMap named `kubelet-config` and all nodes of our cluster (we have only one since we are using Minikube). To edit the ConfigMap, execute this:
```
kubectl edit configmap kubelet-config -n kube-system
```
This will take your terminal window to the configuration file. Here, add the line `serverTLSBootstrap: true` under the line `kind: KubeletConfiguration`. Then save the file and exit.

Next, edit the Kubelet Config On the Kubernetes Node. First, we need to connect to the minikube’s virtual machine (VM) node:
```
minikube ssh
```
Then open the config file located in /var/lib/kubelet/config.yaml with your preferred text editor.
```
sudo vi /var/lib/kubelet/config.yaml
```
Here, add the line `serverTLSBootstrap: true` under the line `kind: KubeletConfiguration`. Then save the file and exit.

Then restart the kubelet service:
```
sudo systemctl restart kubelet
```
Exit the ssh and return to your host. Now restart the metrics-server:
```
kubectl rollout restart deployment metrics-server -n kube-system
```
Then we need to sign the certificates. Run this:
```
kubectl get csr

NAME        AGE   SIGNERNAME                      REQUESTOR              REQUESTEDDURATION   CONDITION
csr-4smqn   29s   kubernetes.io/kubelet-serving   system:node:minikube   <none>              Pending
```
On the right, you can see that the last certificate is waiting for approval. Find its name (`<csr_name>=csr-4smqn` in this case) and run this command:
```
kubectl certificate approve <csr_name>
```
Restart the metrics-server again
```
kubectl rollout restart deployment metrics-server -n kube-system
```
After a while, you can check the status of the metrics-server using the command:
```
kubectl get deployment metrics-server -n kube-system
```

## Clean up the cluster
Specify `-n <namespace>` if needed:
```
kubectl delete deployments --all
kubectl delete services --all
kubectl delete pods --all
kubectl delete daemonset --all
kubectl delete ingress --all
```

## Run
**Run using ingress:**
```
minikube start
# First install and enable the Ingress-Nginx Controller
minikube addons enable ingress
cd web6
kubectl apply -f namespace.yaml
kubectl apply -f secret.yaml
kubectl apply -f mysql.yaml
kubectl apply -f web6.yaml
kubectl apply -f ingress.yaml
minikube tunnel

# add this entry to /etc/hosts
127.0.0.1		web6.pucavv.io.vn
# visit at http://web6.pucavv.io.vn
```
**Run using service:**
```
minikube start
cd web6
kubectl apply -f namespace.yaml
kubectl apply -f secret.yaml
kubectl apply -f mysql.yaml
kubectl apply -f web6.yaml
kubectl apply -f nginx-config.yaml
kubectl apply -f nginx.yaml

# automatically open the browser with the app's address
minikube service nginx-service -n myapp
```
**Spawn an interactive shell inside a pod:**
```
kubectl exec -it <pod_name> -- sh
```
**Copy file from host into pod:**
```
kubectl cp path/to/file <pod_name>:path/to/file/to/copy
```

## Debug
Specify `-n <namespace>` if needed:
```
kubectl describe <name> --watch
kubectl logs <name> --watch
```