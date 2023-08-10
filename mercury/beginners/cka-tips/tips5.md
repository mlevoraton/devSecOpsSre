Get all config form the cluster
kubectl get all --all-namespaces -o yaml > all-deploy-services.yaml


get cluster 

kubectl config view

change cluster 

kubectl config use-context cluster1

if etcd external 
ssh etcd-server