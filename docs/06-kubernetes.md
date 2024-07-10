# Use Kubernetes

The last step is to use our newly created Kubernetes cluster.
To do that we need to download the kubeconfig file from our control plane node with the following command.

```sh
talosctl kubeconfig
```

This will download a kubeconfig file in the default location `$HOME/.kube/config` and now you can inspect your Kubernetes cluster

```sh
kubectl get pods -A
```

You'll notice that the kube-proxy and flannel CNI pods are already deployed in the cluster.

example output

```sh
NAMESPACE     NAME                            READY   STATUS              RESTARTS      AGE
kube-system   coredns-64b67fc8fd-nbqsf        1/1     Running             0             9m31s
kube-system   coredns-64b67fc8fd-rtdhn        1/1     Running             0             9m31s
kube-system   kube-apiserver-k8s-0            1/1     Running             0             7m58s
kube-system   kube-controller-manager-k8s-0   1/1     Running             2 (10m ago)   8m18s
kube-system   kube-flannel-df4js              1/1     Running             0             9m12s
kube-system   kube-flannel-gsh6v              0/1     Init:0/2            0             78s
kube-system   kube-proxy-8t8j7                1/1     Running             0             9m12s
kube-system   kube-proxy-cp4jw                0/1     ContainerCreating   0             78s
kube-system   kube-scheduler-k8s-0            1/1     Running             2 (10m ago)   8m42s

```

Next: [Cleanup](99-cleanup.md)
