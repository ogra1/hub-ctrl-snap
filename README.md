hub-ctrl snap
==========

Control USB power on a port by port basis on some USB hubs from a snap package.

The tool was originally created NIIBE Yutaka and published to Github by Joel Dare at:
https://github.com/codazoda/hub-ctrl.c

This snap works on USB hubs that have the hardware necessary to allow
software controlled power switching. Most hubs DO NOT include the hardware.

Interfaces
=========

Please make sure to connect the ```hardware-observe``` and ```raw-usb``` interfaces after
installing the snap.

    sudo snap connect hub-ctrl:raw-usb
    sudo snap connect hub-ctrl:hardware-observe
    
Building
=========

To compile the hub-ctrl snap run the following command in the top level of this source tree.

    snapcraft

Controlling Power
=================

You can control the power on a port using the following command.

    sudo hub-ctrl -h 3 -P 1 -p 0

That says to control hub 3 (-h 3) port 1 (-P 1) and to turn the power
off (-p 0). You can also use ”-p 1” to turn the power back on.

You can also specify the USB device based on the BUS and DEV numbers. Use the
following command the list the currently connected devices. It's useful to run
this with the device disconnected and then again with the device connected so
that you can tell which device is the one you are trying to target (the Targus
in my case).

    hub-ctrl.lsusb

Now that we know the BUS and DEV numbers, we can control the power using those
numbers as well. Here's the command for that.

    sudo hub-ctrl -b 001 -d 005 -P1 -p 0

This time we are controlling the device on BUS 001 (-b 001) device 005 (-d 005)
port 1 (-P 1) and turning the power off (-p 0).

Hubs Known to Work
==================

The following is a list of Hubs that are known to have the hardware necessary
to allow power switching.

  - D-Link-DUB-H7-High-Speed-7-Port (Tested with old Silver versions (A3, A4 & A5). Also tested with newer Black version C1 although there is one issue reporting that the C1 didn't work).
  - Elecom: U2H-G4S
  - Sanwa Supply: USB-HUB14GPH
  - Targus, Inc.: PAUH212
  - Hawking Technology: UH214
  - B&B Electronics: UHR204
  - Belkin: F5U701
  - Linksys: USB2HUB4
