# Apply the configuration to the machines

In this lab you will apply the configuration we generated in the previous step to both machines that are running in maintenance mode.

## Control plane

We will apply the configuration to the control plane machine first to make sure the Kubernetes services start successfully.
Run this command to configure the machine.

```sh
talosctl apply-config -f controlplane.yaml \
  --nodes $NODE_IP \
  --insecure
```

> The `--insecure` flag is only used in maintenance mode to gather information about the system and configure it.

The on screen dashboard will change after this command is applied, but the machine will still be in a waiting state.
We need to bootstrap the etcd database to get the Kubernetes components running.

Run the following command to bootstrap etcd

```sh
talosctl bootstrap --nodes $CP_IP
```

Now we can wait for the node and Kubernetes components to become healthy.
Run the following command to watch the node health as the components are started.

```sh
talosctl health --control-plane-nodes $CP_IP
```

The output should look something like this.

```
OUTPUT
```

## Worker node

Now that the control plane is up and ready we can apply the configuration to the worker node.

```sh
talosctl apply-config --nodes $WORKER_IP --insecure
```

The node will automatically configure itself to join the Kubernetes cluster.

Next: [Use Kubernetes](06-kubernetes.md)
