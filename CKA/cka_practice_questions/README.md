Practice questions for CKA exam

A kubeconfig file called admin.kubeconfig has been created in /root. There is something wrong with the configuration. Troubleshoot and fix it.

<details><summary>show</summary>
<p>
Make sure the port for the kube-apiserver is correct. Check if the port is 6443.
Run the below command to know the cluster information.

```
kubectl cluster-info --kubeconfig /root/admin.kubeconfig
``` 
</p>p
</details>
