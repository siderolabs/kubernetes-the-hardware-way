# Prerequisites

In this lab you will install the necessary commands needed to create your cluster.

## talosctl

Talos Linux does not have ssh.
All configuration is sent over the Talos machine API and you will need the `talosctl` command installed to interact with the system.

If you are on macOS, Linux, or WSL in Windows you can use [homebrew](https://brew.sh) to install talosctl.

```sh
brew install siderolabs/tap/talosctl
```

If you are on Windows or would like an alternative installation method please refer to [the documentation](https://www.talos.dev/latest/talos-guides/install/talosctl/).

## kubectl

Kubernetes provides a CLI to interact with the API.
If you are on macOS, Linux, or WSL on Windows you can use [homebrew](https://brew.sh) to install kubectl.

```sh
brew install kubectl
```

If you are on Windows or would like an alternative installation method please refer to the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).

Next: [Download Talos Linux](02-download.md)
