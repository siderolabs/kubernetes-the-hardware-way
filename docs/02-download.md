# Download Talos Linux

In this lab you will download Talos Linux.
Talos is going to be installed directly on your machines as the host operating system.
It is also responsible for running the Kubernetes components.

### Download Talos from the image factory

Open your browser to [factory.talos.dev](https://factory.talos.dev) which will walk you through options to download the correct version of Talos for your hardware.

Under the hardware type you can select "bare-metal machine" and click next.
For the screens asking which version, architecture, system extensions, and customization you want to use you can leave the default settings and just click next.

Then you can download the first link which should be an ISO image.

If you don't want to use the web interface you can also download a vanilla copy of Talos Linux 1.7.5 for amd64 architecture with

```sh
wget https://factory.talos.dev/image/376567988ad370138ad8b2698212367b8edcb69b5fd68c80be1f2ec7d603b4ba/v1.7.5/metal-amd64.iso
```

### Install Ventoy

Ventoy is not required but recommended.
It allows you to boot a USB drive with multiple ISOs on it and presents you with a menu for which ISO you want to boot.

This makes it really easy to try different versions of Talos Linux or download versions with different customizations and not have to reformat your USB drive every time.

Ventoy only has an installer from Windows or Linux so if you are on macOS you will need to manually flash your USB drive.

You can download Ventoy for your OS at [Ventoy.net](https://ventoy.net/en/download.html).
Extract the archive and run the `Ventoy2Disk.sh` command and provide your USB drive.

After Ventoy is installed you can just copy the ISO file to your USB drive and it'll be ready to boot.

### Install Etcher (macOS)

Etcher is a GUI application for writing disk images to a USB drive.
You can download it from [etcher.balena.io](https://etcher.balena.io/) and install it on your system.

Launch the program and select your ISO file and USB drive to flash the device.
It should now be ready to boot on your machines.

Next: [Boot Talos Linux](03-boot.md)
