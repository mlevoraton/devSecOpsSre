etcdctl is a command line client for etcd.


In all our Kubernetes Hands-on labs, the ETCD key-value database is deployed as a static pod on the master. The version used is v3.

To make use of etcdctl for tasks such as back up and restore, make sure that you set the ETCDCTL_API to 3.


You can do this by exporting the variable ETCDCTL_API prior to using the etcdctl client. This can be done as follows:

export ETCDCTL_API=3

On the Master Node:
export ETCDCTL_API=3
etcdctl version

To see all the options for a specific sub-command, make use of the -h or --help flag.


For example, if you want to take a snapshot of etcd, use:

etcdctl snapshot save -h and keep a note of the mandatory global options.


Since our ETCD database is TLS-Enabled, the following options are mandatory:

--cacert                                                verify certificates of TLS-enabled secure servers using this CA bundle

--cert                                                    identify secure client using this TLS certificate file

--endpoints=[127.0.0.1:2379]          This is the default as ETCD is running on master node and exposed on localhost 2379.

--key                                                      identify secure client using this TLS key file



Similarly use the help option for snapshot restore to see all available options for restoring the backup.

etcdctl snapshot restore -h

For a detailed explanation on how to make use of the etcdctl command line tool and work with the -h flags, check out the solution video for the Backup and Restore Lab.

call etc logs
root@controlplane:~# kubectl -n kube-system logs etcd-controlplane | grep -i 'etcd-version'
"caller":"embed/etcd.go:306","msg":"starting an etcd server","etcd-version":"3.5.7","git-sha":"215b53cf3"

root@controlplane:~# 

root@controlplane:~# kubectl -n kube-system describe pod etcd-controlplane | grep Image:
    Image:         registry.k8s.io/etcd:3.5.7-0
root@controlplane:~#

get etcdctl url 
ot@controlplane:~# kubectl -n kube-system describe pod etcd-controlplane | grep '\--listen-client-urls'
      --listen-client-urls=https://127.0.0.1:2379,https://10.2.43.11:2379
root@controlplane:~#
get certificate 
kubectl -n kube-system describe pod etcd-controlplane | grep '\--cert-file'
get ca certificate 
kubectl -n kube-system describe pod etcd-controlplane | grep '\--peer-trusted-ca-file'