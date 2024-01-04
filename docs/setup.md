# Cluster Setup

### Follow the onedr0p installation with the additional steps below

<details>
  <summary>Rename all network interfaces</summary>
  <br>

1. Change the name of the network interface to Eth0 (easier to reference if they all have the same name)

    ###### Renaming Interfaces with udev Rules:

      Find the current name and hardware address of your interfaces:
      Run ```ip link``` or ```ifconfig``` to list all network interfaces.
      Note down the MAC address of the interface you want to rename.

    ##### Create a Custom udev Rule:

      Edit/Create the udev rules file:
      Create or edit a file in the /etc/udev/rules.d/ directory, e.g., 10-persistent-network.rules
      Use a text editor like nano or vim:

       sudo nano /etc/udev/rules.d/10-persistent-network.rules

    ##### Add your custom rule:
      Write a rule to match the MAC address and assign a name:

       SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="eth0"

      Replace aa:bb:cc:dd:ee:ff with the actual hardware (MAC) address of your network interface and eth0 with the desired name.

    ##### Apply the Changes:

      ```Run sudo udevadm control --reload-rules && sudo udevadm trigger``` to apply the changes without rebooting.

      Reboot (optional but recommended):

      Reboot your system to ensure that the changes take effect and that the interface is correctly renamed on startup: sudo reboot

   ##### Update Network Configuration:
      Once you've renamed your interfaces, you'll need to update your network configuration to reflect the new names.
      Edit the network configuration files, which might be located in /etc/network/interfaces or /etc/netplan/ for newer systems.
      Replace any instance of the old interface name with the new one.
</details>
