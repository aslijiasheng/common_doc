# pod相关操作
```bash
kubectl get pod -A
kubectl get pod -n {namespace} -owide

kubectl get po -a --all-namespaces -o json | jq  '.items[] | select(.status.reason!=null) | select(.status.reason | contains("Evicted")) | "kubectl delete po \(.metadata.name) --n \(.metadata.namespace)"' | xargs -n 1 bash -c

kubectl get po -a --all-namespaces -o json --field-selector="status.phase!=Running" | jq  '.items[]  | "kubectl delete po \(.metadata.name) --n \(.metadata.namespace)"' | xargs -n 1 bash -c


kubectl get po -a --all-namespaces -o json | \
jq  '.items[] | select(.status.reason!=null) | select(.status.reason | contains("Evicted")) |
"kubectl delete po \(.metadata.name) -n \(.metadata.namespace)"' | xargs -n 1 bash -c


#!/bin/bash
for each in $(kubectl get pods|grep Evicted|awk '{print $1}');
do
kubectl delete pods $each
done


kubectl get pods --field-selector=status.phase=Failed | awk '{ if(NR>1)print $1}' | xargs kubectl delete pods
kubectl get pods -n kube-system| grep Evicted | awk '{print $1}' | xargs kubectl delete pod
kubectl get pods --all-namespaces| grep Evicted | $(awk '{print "kubectl -n " $1 " delete pod "$2}')
```
## 查看pod详情
```
kubectl describe pod {podname} -n {namespace}
```
## 查看Pod的日志
```bash
kubectl logs -f {podname} -n {namespace}
kubectl -n {namesapce} logs -f deployment/{podname} --all-containers=true --since=10m
```
## Copy Files from a pod to your machine
```bash
kubectl cp {{namespace}}/{{podname}}:path/to/directory /local/path
```
## 查看configmaps的方法
```bash
kubectl get configmaps game-config -o yaml
```
# delete Evicted status pod
```bash
kubectl get pods | grep Evicted | awk '{print $1}' | xargs kubectl delete pod
```



# ingress
[canary deployment with ingress-nginx](https://www.elvinefendi.com/2018/11/25/canary-deployment-with-ingress-nginx.html)

## 查看ingress
```bash
kubectl get ing -A
```

# Apply
```bash
kubectl apply -f ./my-manifest.yaml 
```

# Viewing, Finding Resources
```bash
# Get commands with basic output
kubectl get services                          # List all services in the namespace
kubectl get pods --all-namespaces             # List all pods in all namespaces
kubectl get pods -o wide                      # List all pods in the current namespace, with more details
kubectl get deployment my-dep                 # List a particular deployment
kubectl get pods                              # List all pods in the namespace
kubectl get pod my-pod -o yaml                # Get a pod's YAML

# Describe commands with verbose output
kubectl describe nodes my-node
kubectl describe pods my-pod

# List Services Sorted by Name
kubectl get services --sort-by=.metadata.name

# List pods Sorted by Restart Count
kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'

# List PersistentVolumes sorted by capacity
kubectl get pv --sort-by=.spec.capacity.storage

# Get the version label of all pods with label app=cassandra
kubectl get pods --selector=app=cassandra -o \
  jsonpath='{.items[*].metadata.labels.version}'

# Get all worker nodes (use a selector to exclude results that have a label
# named 'node-role.kubernetes.io/master')
kubectl get node --selector='!node-role.kubernetes.io/master'

# Get all running pods in the namespace
kubectl get pods --field-selector=status.phase=Running

# Get ExternalIPs of all nodes
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'

# List Names of Pods that belong to Particular RC
# "jq" command useful for transformations that are too complex for jsonpath, it can be found at https://stedolan.github.io/jq/
sel=${$(kubectl get rc my-rc --output=json | jq -j '.spec.selector | to_entries | .[] | "\(.key)=\(.value),"')%?}
echo $(kubectl get pods --selector=$sel --output=jsonpath={.items..metadata.name})

# Show labels for all pods (or any other Kubernetes object that supports labelling)
kubectl get pods --show-labels

# Check which nodes are ready
JSONPATH='{range .items[*]}{@.metadata.name}:{range @.status.conditions[*]}{@.type}={@.status};{end}{end}' \
 && kubectl get nodes -o jsonpath="$JSONPATH" | grep "Ready=True"

# List all Secrets currently in use by a pod
kubectl get pods -o json | jq '.items[].spec.containers[].env[]?.valueFrom.secretKeyRef.name' | grep -v null | sort | uniq

# List all containerIDs of initContainer of all pods
# Helpful when cleaning up stopped containers, while avoiding removal of initContainers.
kubectl get pods --all-namespaces -o jsonpath='{range .items[*].status.initContainerStatuses[*]}{.containerID}{"\n"}{end}' | cut -d/ -f3

# List Events sorted by timestamp
kubectl get events --sort-by=.metadata.creationTimestamp

# Compares the current state of the cluster against the state that the cluster would be in if the manifest was applied.
kubectl diff -f ./my-manifest.yaml
```

# Interacting with running Pods
```bash
kubectl logs my-pod                                 # dump pod logs (stdout)
kubectl logs -l name=myLabel                        # dump pod logs, with label name=myLabel (stdout)
kubectl logs my-pod --previous                      # dump pod logs (stdout) for a previous instantiation of a container
kubectl logs my-pod -c my-container                 # dump pod container logs (stdout, multi-container case)
kubectl logs -l name=myLabel -c my-container        # dump pod logs, with label name=myLabel (stdout)
kubectl logs my-pod -c my-container --previous      # dump pod container logs (stdout, multi-container case) for a previous instantiation of a container
kubectl logs -f my-pod                              # stream pod logs (stdout)
kubectl logs -f my-pod -c my-container              # stream pod container logs (stdout, multi-container case)
kubectl logs -f -l name=myLabel --all-containers    # stream all pods logs with label name=myLabel (stdout)
kubectl run -i --tty busybox --image=busybox -- sh  # Run pod as interactive shell
kubectl run nginx --image=nginx --restart=Never -n 
mynamespace                                         # Run pod nginx in a specific namespace
kubectl run nginx --image=nginx --restart=Never     # Run pod nginx and write its spec into a file called pod.yaml
--dry-run -o yaml > pod.yaml

kubectl attach my-pod -i                            # Attach to Running Container
kubectl port-forward my-pod 5000:6000               # Listen on port 5000 on the local machine and forward to port 6000 on my-pod
kubectl exec my-pod -- ls /                         # Run command in existing pod (1 container case)
kubectl exec my-pod -c my-container -- ls /         # Run command in existing pod (multi-container case)
kubectl top pod POD_NAME --containers               # Show metrics for a given pod and its containers
kubectl exec  -it ay1688-devwxstore-legacy-service-devwechat-deployment-5d6ctzzqs bash -nay1688
```

# Interacting with Nodes and Cluster
```
kubectl cordon my-node                                                # Mark my-node as unschedulable
kubectl drain my-node                                                 # Drain my-node in preparation for maintenance
kubectl uncordon my-node                                              # Mark my-node as schedulable
kubectl top node my-node                                              # Show metrics for a given node
kubectl cluster-info                                                  # Display addresses of the master and services
kubectl cluster-info dump                                             # Dump current cluster state to stdout
kubectl cluster-info dump --output-directory=/path/to/cluster-state   # Dump current cluster state to /path/to/cluster-state

# If a taint with that key and effect already exists, its value is replaced as specified.
kubectl taint nodes foo dedicated=special-user:NoSchedule
```