# Commands

## SSH

To find SSH information for devices:
1. Find the 'Device Updates and Settings' section on the bottom left corner of the UniFi Devices menu.
2. SSH Username and Password are written in the bottom right corner of the new popup window.
3. Login using `ssh username@IP_Address`
![SSH Information](/unifi/assets/SSH_UNPW.png)

## UniFi SSH Commands

Command | Example        | Function
--------|----------------|---------
info    | `info`           | Displays device information
set-default | `set-default` | Factory reset device
set-inform | `set-inform http://192.168.1.1:8080/inform` | Set URL of the controller for adoption.
upgrade | `upgrade https://<firmware-url>.bin` | Upgrade firmware
fwupdate | `fwupdate --url https://<firmware-url>.bin` | Update firmware
reboot  | `reboot`         | Reboot the device
poweroff | `poweroff`      | Shutdown device
uptime  | `uptime`         | Shows device uptime

## Network Related SSH Commands

Command  | Example   | Function
---------|-----------|---------
ifconfig | `ifconfig` | Show network interface information
ip address add | `ip address add 192.168.1.143/24 dev br0` | Set static IP Address
ip route | `ip route` | Display current gateway
ip router add | `ip route add default via 192.168.1.1` | Set default gateway
 ... | `echo "nameserver 192.168.1.1" > /etc/resolv.conf` | Set DNS Server
ping | `ping 1.1.1.1` | Check network connection to device
arp | `arp -a` | Show arp table
ip neigh | `ip neigh`  | Show IPv6 neighbors

## UniFi OS SSH Commands

Command  | Example   | Function
---------|-----------|---------
ubnt-systool help | `ubnt-systool help` | Show all commands
ubnt-systool cputemp | `ubnt-systool cputemp` | Show CPU Temp
ubnt-systool cpuload | `ubnt-systool cpuload` | Show CPU load
ubnt-systool portstatus | `ubnt-systool portstatus` | Show port status
ubnt-systool hostname | `ubnt-systool hostname <newname>` | Set new hostname
ubnt-systool reboot | `ubnt-systool reboot`  | Reboot device
ubnt-systool poweroff | `ubnt-systool poweroff` | Shutdown device
ubnt-systool reset2defaults | `ubnt-systool reset2defaults`  | Factory reset device
ubnt-device-info summary | `ubnt-device-info summary` | Show system information
ubnt-tools ubnt-discover | `ubnt-tools ubnt-discover` | Show Unifi devices in the network
cat /mnt/data/udapi-config/dnsmasq.lease | `cat /mnt/data/udapi-config/dnsmasq.lease` | Show DHCP Leases
cat /mnt/data/udapi-config/unifi | `cat /mnt/data/udapi-config/unifi` | Show configuration
/etc/init.d/S95unifios restart | `/etc/init.d/S95unifios restart` | Restart Unifi OS Web interface

## UniFi Log Files

Command  |Function
---------|---------
`cat /var/log/messages` | Output the error log
`tail -f /var/log/messages` | Monitor log file
`cat /mnt/data/unifi-os/unifi-core/config/settings.yaml` | Server settings
`cat /mnt/data/unifi-os/unifi-core/logs/discovery.log` | Discovery log
`cat /mnt/data/unifi-os/unifi-core/logs/system.log` | System log
`cat /mnt/data/unifi-os/unifi/logs/server.log` | Server log
`cat /mnt/data/unifi-os/unifi-core/logs/errors.log` | Http errors

## Other Useful Commands

Command | Function | More Info
--------|----------|----------
`syswrapper.sh restore-default` | Restore Syswrapper | When it boots but doesn't work
`/sbin/udhcpc -f -i eth0 -s /etc/udhcpc/udhcpc -p /var/run/udhcpc.eth0.pid` | Renew dhcp/dns | Where eth0 is the interface to renew found by running `ip route`

## Network Devices

To turn on/off switch port lights on USW-Lite-8-PoE:
`swctrl led set on/off`

*All sources found [HERE](https://lazyadmin.nl/home-network/unifi-ssh-commands/)*

## Installing Unifi Network Application to Debian and Ubuntu

### Update package lists, upgrade all packages, and remove unnecessary packages
``` bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

### Install required packages
``` bash
sudo apt install -y gnupg curl ca-certificates apt-transport-https
```

### Add MongoDB GPG key and repository
``` bash
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
echo "deb [ arch=amd64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] http://repo.mongodb.org/apt/debian bookworm/mongodb-org/7.0 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
```

### Add Unifi GPG key and repository
``` bash
curl -fsSL https://dl.ui.com/unifi/unifi-repo.gpg | sudo gpg -o /usr/share/keyrings/unifi-repo.gpg --dearmor
echo 'deb [ arch=amd64 signed-by=/usr/share/keyrings/unifi-repo.gpg ] https://www.ui.com/downloads/unifi/debian stable ubiquiti' | sudo tee /etc/apt/sources.list.d/unifi.list
```

### Update package lists again to include the new repositories
``` bash
sudo apt update
```
 
### Install MongoDB and Unifi
``` bash
sudo apt install -y mongodb-org
sudo apt install -y unifi
```

*Source found [HERE](https://www.reddit.com/r/UNIFI/comments/1deaeoj/how_to_guide_installing_unifi_network_application/)*
