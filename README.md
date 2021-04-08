# Netplan-Ubuntu18up
Update to changes network interfaces respository

# Netplan

## The network configuration abstraction renderer

Netplan is a utility for easily configuring networking on a linux system. You simply create a YAML description of the required network interfaces and what each should be configured to do. From this description Netplan will generate all the necessary configuration for your chosen renderer tool.

## How does it work?

Netplan reads network configuration from **/etc/netplan/*.yaml** *which are written by administrators, installers, cloud image instantiations, or other OS deployments. During early boot, Netplan generates backend specific configuration files in /run to hand off control of devices to a particular networking daemon.*

![image](https://user-images.githubusercontent.com/79214343/114074174-4a2bc700-98ce-11eb-9118-e857d163b1fd.png)


Netplan currently works with these supported renderers
  
  * [NetworkManager](https://help.ubuntu.com/community/NetworkManager)
  * [Systemd-networkd](https://manpages.ubuntu.com/manpages/bionic/man5/systemd.network.5.html)


## How do I use it?

### Configuration
```
network:
  version: 2
    renderer: NetworkManager
 ```

This will make NetworkManager manage all devices (and by default, any ethernet device will come up with DHCP once carrier is detected).

Using networkd as a renderer does not let devices automatically come up using DHCP; each interface needs to be specified in a file in **/etc/netplan** for its configuration to be written and for it to be used in networkd.

### Commands

Netplan uses a set of subcommands to drive its behavior:

- [x] **netplan generate**: Use **/etc/netplan** to generate the required configuration for the renderers.
- [x] **netplan apply**: Apply all configuration for the renderers, restarting them as necessary.
- [x] **netplan try**: Apply configuration and wait for user confirmation; will roll back if network is broken or no confirmation is given.
