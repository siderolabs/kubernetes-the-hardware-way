# Boot Nodes

You now have a USB drive with Talos Linux and a couple machines plugged in to power and network.
You'll want a monitor, keyboard, and mouse plugged in to the computers when you boot them.
Let's Go!!!

## Boot 1st machine

Plug in your USB drive and boot the first machine.
If the machine previously had an operating system installed you will likely need to push a F key on your keyboard to load the boot menu.

Common keys are F12 or Delete.
If that doesn't work you may need to change the boot order in your systems BIOS.
Please search how to do that for your particular computer or motherboard.

When the machine boots it will show the Ventoy menu (assuming you used Ventoy).
You can select the Talos ISO from the menu, usually called metal-amd64.

On the second menu select "Boot in Normal Mode" to continue booting the ISO.

This should start the boot process from the USB drive and you will likely see some penguins (named Tux) on top of your screen and a bunch of text.

The machine will eventually boot to the Talos dashboard.
This has a lot of useful information related to the machine state (should read maintenance) and the network connection information.

You'll need the network information for a step in the future so make note of it.

If the machine reached the dashboard you can pull out the USB drive.
The operating system is running completely in memory and the USB drive is no longer needed.

The machine will wait in maintenance mode until it's told to install itself.

## Boot 2nd machine

Follow the same steps to boot the second machine.
All of the steps will be the same and once the machine gets to the dashboard you can remove the USB drive.

Next: [Generate Config](04-config.md)
