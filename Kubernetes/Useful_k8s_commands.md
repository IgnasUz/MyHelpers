# Useful Kubernetes commands

## Useful for Debuging
* `kubectl get pods -o wide` - list all pods in the current namespace, with more details
* `kubectl describe pods <pod-name>` - get pod details with verbose output (Event, statuses, IP, etc.)
* `kubectl get events --sort-by=.metadata.creationTimestamp` - list events sorted by timestamp
* `kubectl logs <pod-name>` - gets the logs of the application (running in the POD)
* `kubectl exec -it <pod-name> -- bin/bash` -> gets the terminal of the application container and run commands there

## Get Command list

### Pod
* `kubectl get pods` - list all pods in the namespace
* `kubectl get pods -A` - get all pods from all namespaces
* `kubectl get pods -o wide` - list all pods in the current namespace, with more details
* `kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'` - list pods sorted by restart count
* `kubectl get pods --field-selector=status.phase=Running` - get all running pods in the namespace
* `kubectl get pods --show-labels` - show labels for all pods (or any other Kubernetes object that supports labelling)
* `kubectl get pod <pod-name> -o yaml` - get a pod's YAML
* `kubectl describe pods <pod-name>` - get pod with verbose output (Event, statuses, IP, etc.)

### Deployment
* `kubectl get deployment <deployment-name>` - get a specified deployment
* `kubectl get deployment` - lists deployments in the namspace
* `kubectl get deployment -A` - lists deployments from all namespaces
* `kubectl get deployment <deployment-name> -o yaml` - gets the configuration of the deployment (from etcd key-value storage) in YAML format
* `kubectl get deployment <deployment-name> -o yaml > <file-name.yaml>` - output the configuration of the deployment to a new YAML file

### Replicaset 
* `kubectl get replicaset <replicaset-name>` - get a specified replica set
* `kubectl get replicaset` - lists replica sets in the namspace
* `kubectl get replicaset -A`- lists replica sets from all namespaces

### Services
* `kubectl get services <service-name>` - get specified service
* `kubectl get services` - list services in the namspace
* `kubectl get services --sort-by=.metadata.name` - list services sorted by name
* `kubectl get services -A` - list services from all namespaces

### Node 
* `kubectl get nodes` - list nodes in the namspace
* `kubectl describe nodes <node-name>` - get node details with verbose output (Event, statuses, IP, etc.)
* `kubectl get node --selector='!node-role.kubernetes.io/master'` - get all worker nodes (use a selector to exclude results that have a label named 'node-role.kubernetes.io/master')

### Persistent Volumes
* `kubectl get pv` - list persistent volumes
* `kubectl get pv --sort-by=.spec.capacity.storage` - list persistent volumes sorted by capacity

### Config Map
* `kubectl get configmap <config-map-name>` - get specified config map
* `kubectl get configmap` - list all configmaps in the namspace
* `kubectl get configmap -A`- list all secrects from all namespaces

### Secrets
* `kubectl get secrets <secret-name>` - get specified secret
* `kubectl get secrets` - list all secrects for namspace
* `kubectl get secrets -A` - list all secrects from all namespaces


## Other
* `kubectl version` - display kubernetes client version and kubernetes server version

## Create/Modify Command List
* `kubectl create <component>` - creates different components
* `kubectl create deployment <deployment-name> --image=<image>` - creates a deployment with a specified name from a specified image (e.g. `kubectl create deployment my-deployment-name --image=nginx`)
* `kubectl deployment edit <deployment-name>` - opens deployment configuration file, where you can edit it
* `kubectl apply -f <file-name>` - takes a configuration file and applies whatever is in it
* 
> Usually `kubectl create` or `kubectl edit` should be used for testing purposes only. You should use YAML configuration files instead and run `kubectl apply <configuration-file-name>`.

## Minikube
* `minikube start --driver=docker` - start cluster with specific driver (docker in this case)
* `minikube config set driver docker` - set the default driver (`minkube start` will use it as a default)
* `minkube start --memory <MB-value> --cpus <CPU-count>` - specify cluster resources (default is 2200Mb / 2 CPUs)
* `minkube status` - gets the status of a local kubernetes cluster
* `minikube dashboard` - run minikube dashboard and open it in the browser automatically (dashboard is used to manage and monitor health of the cluster)
* `minikube dashboard` - run minikube dashboard but returns only the URL (doesn't open it automatically)
* `minikube delete --all` - deletes all minikube clusters
> Minikube is usually used for setting up local cluster for testing purposes. Resource: https://minikube.sigs.k8s.io/docs/start/.


===========================================================

* kubectl get services                          # List all services in the namespace
kubectl get pods --all-namespaces             # List all pods in all namespaces
kubectl get pods -o wide                      # List all pods in the current namespace, with more details
kubectl get deployment my-dep                 # List a particular deployment
                         # List all pods in the namespace
kubectl get pod my-pod -o yaml                # Get a pod's YAML



* `kubectl get pod -o wide` - get a list of pods with additional details like IPs
* `kubectl get events --sort-by=.metadata.creationTimestamp` - get a list of events sorted by timestamp
* `kubectl get deployment <deployment-name>` - 



JSONPATH='{range .items[*]}{@.metadata.name}:{range @.status.conditions[*]}{@.type}={@.status};{end}{end}' \ && kubectl get nodes -o jsonpath="$JSONPATH" | grep "Ready=True"


i. kubectl version -> display Client K8s version and Server k8s version
ii. kubectl get pods -A -> list the requested objects (pods) across all namespaces
iv. kubectl get nodes
v. kubectl get services
vi. kubectl get deployment <deployment-name> -o yaml -> gets the updated configuration of the deployment (from etcd key-value storage)
vii. kubectl get deployment <deployment-name> -o yaml > <file-name.yaml> -> output the above command into a file.
viii. kubectl create <component> -> creates different components
1) kubectl create deployment <Name> --image=<image> -> more info above
2) kubectl get replicaset -> get replicaset (replicaset is managing the replicas of a POD, but user will not be working with replicasets, but rather with deployments)
3) Layers of abstraction: deployment -manages-> replicaset -manages-> POD -abstraction-> container (anything below the deployment, should be managed by Kubernetes)
ix. kubectl deployment edit <deployment-name> -> opens deployment configuration file, where you can edit it
x. kubectl apply -f <file-name> -> takes a configuration file and applies whatever is in it
xi. Debugging: 
1) kubectl logs <pod-name> -> gets the logs of the application (running in the POD)
2) kubectl describe pod <pod-name> -> Show details of a specific resource (in this case POD) or group of resources
3) kubectl exec -it <pod-name> -- bin/bash -> gets the terminal
