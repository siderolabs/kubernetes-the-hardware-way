# Use Kubernetes

The last step is to use our newly created Kubernetes cluster.
To do that we need to download the kubeconfig file from our control plane node with the following command.

```sh
talosctl kubeconfig . --endpoints "$CP_IP"
```

This will download a `kubeconfig` file in your local directory.
You can configure `kubectl` to use this file with

```sh
export KUBECONFIG=$PWD/kubeconfig
```

and now you can inspect your Kubernetes cluster

```sh
kubectl get pods -A
```

You'll notice that the kube-proxy and flannel CNI pods are already deployed in the cluster.
