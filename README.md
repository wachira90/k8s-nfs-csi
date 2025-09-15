# k8s-nfs-csi

k8s-nfs-csi




# Common Issues

1. The NFS CSI controller and node pods are getting stuck in `Pending` state

Make sure that you specify 

```sh
--set kubeletDir=/var/snap/microk8s/common/var/lib/kubelet 
```

when installing the Helm chart.


2. I created the nfs-csi storage class, but cannot provision volumes

Double-check that you have specified the NFS server IP address and share path correctly. Also, make sure that your MicroK8s node can mount NFS shares. If you are running a cluster, all MicroK8s nodes should be allowed to mount NFS shares.

3. Provisioning new volumes fails, but I've done everything else correctly

Check the logs of the command 

```sh
nfs
```

containers in the controller and node pods, using the following commands:

```sh
microk8s kubectl logs --selector app=csi-nfs-controller -n kube-system -c nfs
microk8s kubectl logs --selector app=csi-nfs-node -n kube-system -c nfs
```
The logs should help with debugging any issues.
