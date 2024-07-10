# Generate cluster and machine config

In this lab you will generate the configuration for your Talos Linux machines and Kubernetes cluster.
All of these steps will be run from your primary computer where you have `talosctl` installed.

## Gen config

The `talosctl` command has a helpful command to create config files for your machines.
But first we need a little bit of information from your machines to make sure the installation works.

### Get hard drive information

Everything in Talos Linux is an API and you can get your disk information from the following command.

> If you left your USB drive plugged in it will show up in the output for this command. It's easier to remove the USB drive first so you're not confused on which disk to use.

```sh
talosctl disks --insecure --nodes $CP_IP
talosctl disks --insecure --nodes $WORKER_IP
```

> Make sure you run this command against both of your machines. If they have different install disks you will need to edit the proper configuration files below.

The output of this command will look something like this.

```sh
DEV            MODEL                            SERIAL         TYPE   UUID                                   WWID                                   MODALIAS   NAME   SIZE     BUS_PATH                                                   SUBSYSTEM          READ_ONLY   SYSTEM_DISK
/dev/nvme0n1   WDC PC SN720 SDAPNTW-512G-1006   2008A0809615   NVME   e8238fa6-bf53-0001-001b-448b46abe2b3   eui.e8238fa6bf530001001b448b46abe2b3   -          -      512 GB   /pci0000:00/0000:00:1d.0/0000:02:00.0/nvme/nvme0/nvme0n1   /sys/class/block
```

With this output you can export the device path for your primary hard drive where you want to install the operating system.

> NOTE: These are just examples. Use the devices from your machine output

```sh
export CP_DEV=/dev/nvme0n1
export WORKER_DEV=/dev/sda
```

Now we want to generate our config file for the cluster.
This command will generate 3 files in the current directory.

```sh
talosctl gen config k8s-the-hardware-way https://k8s-0:6443 \
  --additional-sans $CP_IP
```

The `controlplane.yaml` configuration will be applied to machines that should run the Kubernetes control plane components (eg API server, controller manager, scheduler).

The `worker.yaml` configuration will be applied to machines that should run the Kubernetes worker components (eg kubelet, kube-proxy).

The `talosconfig` file is used to authenticate `talosctl` commands to the Talos API after the machine has been provisioned.

## Set a stable machine name and install disk

In the `gen config` command we set an additional SAN for the Kubernetes certificate with the IP address of the system.
The problem with using this in environments with DHCP is the IP address might change when the machine reboots.
To avoid that we are going to use the DNS name `k8s-0`.
We also need to configure the machine to set that hostname during installation.

We can create a patch file to modify the default configuration for the control plane and worker node.

```yaml
cat << EOF > cp-patch.yaml
machine:
    network:
        hostname: k8s-0
    install:
        disk: $CP_DEV
EOF

cat << EOF > worker-patch.yaml
machine:
    install:
        disk: $WORKER_DEV
EOF
```

This assumes that you have working DNS on your network.
If your DNS resolution to hosts isn't stable then you may want to configure your router to set an IP address reservation for the machine or configure a static IP address in the config.

If you cannot do either of those things you can also [try setting a virtual IP address (VIP)](https://www.talos.dev/latest/reference/configuration/v1alpha1/config/#Config.machine.network.interfaces..vip) for your node to broadcast a static IP address on the network.

Next: [Apply the configuration to the machines](05-apply-config.md)
