# Apply the configuration to the machines

In this lab you will apply the configuration we generated in the previous step to both machines that are running in maintenance mode.

## Control plane

We will apply the configuration to the control plane machine first to make sure the Kubernetes services start successfully.
Run this command to configure the machine.

```sh
talosctl apply-config -f controlplane.yaml \
  --nodes $CP_IP \
  --config-patch "@cp-patch.yaml" \
  --insecure
```

> The `--insecure` flag is only used in maintenance mode to gather information about the system and configure it.

The on screen dashboard will change after this command is applied, but the machine will still be in a waiting state.

Export your new `talosconfig` file to use with `talosctl` commands and configure it to use the new node and endpoint by default.

```sh
export TALOSCONFIG=$(pwd)/talosconfig
talosconfig config endpoint $CP_IP
talosconfig config node $CP_IP
```

We need to bootstrap the etcd database to get the Kubernetes components running.

Run the following command to bootstrap etcd

```sh
talosctl bootstrap
```

Now we can wait for the node and Kubernetes components to become healthy.
Run the following command to watch the node health as the components are started.

```sh
talosctl health
```

The output should look something like this.

```
discovered nodes: ["192.168.4.26"]
waiting for etcd to be healthy: ...
waiting for etcd to be healthy: 1 error occurred:
        * 192.168.4.26: service is not healthy: etcd
waiting for etcd to be healthy: OK
waiting for etcd members to be consistent across nodes: ...
waiting for etcd members to be consistent across nodes: OK
waiting for etcd members to be control plane nodes: ...
waiting for etcd members to be control plane nodes: OK
waiting for apid to be ready: ...
waiting for apid to be ready: OK
waiting for all nodes memory sizes: ...
waiting for all nodes memory sizes: OK
waiting for all nodes disk sizes: ...
waiting for all nodes disk sizes: OK
waiting for kubelet to be healthy: ...
waiting for kubelet to be healthy: OK
waiting for all nodes to finish boot sequence: ...
waiting for all nodes to finish boot sequence: OK
waiting for all k8s nodes to report: ...
waiting for all k8s nodes to report: Get "https://192.168.4.26:6443/api/v1/nodes": dial tcp 192.168.4.26:6443: connect: connection refused
waiting for all k8s nodes to report: can't find expected node with IPs ["192.168.4.26" "fd51:f76a:6a2f:1:cad9:d2ff:fe00:9000" "fd77:2d8c:3879:d64c:cad9:d2ff:fe00:9000"]
waiting for all k8s nodes to report: OK
waiting for all k8s nodes to report ready: ...
waiting for all k8s nodes to report ready: some nodes are not ready: [k8s-0]
waiting for all k8s nodes to report ready: OK
waiting for all control plane static pods to be running: ...
waiting for all control plane static pods to be running: OK
waiting for all control plane components to be ready: ...
waiting for all control plane components to be ready: expected number of pods for kube-apiserver to be 1, got 0
waiting for all control plane components to be ready: OK
waiting for kube-proxy to report ready: ...
waiting for kube-proxy to report ready: OK
waiting for coredns to report ready: ...
waiting for coredns to report ready: OK
waiting for all k8s nodes to report schedulable: ...
waiting for all k8s nodes to report schedulable: OK
```

## Worker node

Now that the control plane is up and ready we can apply the configuration to the worker node.

```sh
talosctl apply-config --nodes $WORKER_IP \
  --file worker.yaml \
  --config-patch "@worker-patch.yaml" \
  --insecure
```

The node will automatically configure itself to join the Kubernetes cluster.

Next: [Use Kubernetes](06-kubernetes.md)
