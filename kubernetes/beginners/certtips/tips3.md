Label Nodes

kubectl label nodes <node-name> <label-key>=<key-value>
kubectl label nodes node-1 size=Large

Edit deployments

kubectl edit deployment/my-nginx

A quick note on editing Pods and Deployments
Edit a POD

Remember, you CANNOT edit specifications of an existing POD other than the below.

    spec.containers[*].image

    spec.initContainers[*].image

    spec.activeDeadlineSeconds

    spec.tolerations

For example you cannot edit the environment variables, service accounts, resource limits (all of which we will discuss later) of a running pod. But if you really want to, you have 2 options:

1. Run the kubectl edit pod <pod name> command.  This will open the pod specification in an editor (vi editor). Then edit the required properties. When you try to save it, you will be denied. This is because you are attempting to edit a field on the pod that is not editable.

A copy of the file with your changes is saved in a temporary location as shown above.

You can then delete the existing pod by running the command:

kubectl delete pod webapp


Then create a new pod with your changes using the temporary file

kubectl create -f /tmp/kubectl-edit-ccvrq.yaml


2. The second option is to extract the pod definition in YAML format to a file using the command

kubectl get pod webapp -o yaml > my-new-pod.yaml

Then make the changes to the exported file using an editor (vi editor). Save the changes

vi my-new-pod.yaml

Then delete the existing pod

kubectl delete pod webapp

Then create a new pod with the edited file

kubectl create -f my-new-pod.yaml


Edit Deployments

With Deployments you can easily edit any field/property of the POD template. Since the pod template is a child of the deployment specification,  with every change the deployment will automatically delete and create a new pod with the new changes. So if you are asked to edit a property of a POD part of a deployment you may do that simply by running the command

kubectl edit deployment my-deployment 

Copy configuration of another pod

kubectl get po elephant -o yaml > elephant.yaml

describe daemonset\

kubectl describe daemonset kube-proxy --namespace=kube-system

create daemonset

An easy way to create a DaemonSet is to first generate a YAML file for a Deployment with the command kubectl create deployment elasticsearch --image=registry.k8s.io/fluentd-elasticsearch:1.20 -n kube-system --dry-run=client -o yaml > fluentd.yaml. Next, remove the replicas, strategy and status fields from the YAML file using a text editor. Also, change the kind from Deployment to DaemonSet.

create a pod with sleep 
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml

get logs from scheduler 

kubectl logs scheduler --namespace=namespace

Get all namespaces serviceaccounts

kubectl get serviceaccounts -n kube-system

Get entities and their role binding

kubectl get clusterrolebinding

kubernetes metrics server 
git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git

get metrics form metrics server 
kubectl top pods
kubectl top nodes