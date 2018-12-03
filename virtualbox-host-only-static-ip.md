### VirtualBox Host-Only Static IP

My typical setup for a development box in [VirtualBox](https://www.virtualbox.org/) uses two NICs. The first uses NAT to allow the box to communicate with the outside world through my host computer’s network connection. (NAT is the default, so shouldn't require any setup.) The second is a "host-only" connection that allows my host and guest to interact.

To create a host-only connection in VirtualBox, start by opening the preferences in VirtualBox. Go to the "Network" tab, and addd a Host-only Network. Modify the host-only network, and disable DHCP. Make a note of the IP address. (Feel free to set the IP address as well, if you like.)

Next, assign this host-only adapter to the virtual machine. Select the VM and press "Settings". Go to the "Network" tab, and select "Adpater 2". Enable the adapter, set it to a "Host-only Adapter", and select the adpater you created above.

### Temporary

To get the static IP address working temporarily, access the termainal on the client, and enter the following to assign a static IP to eth1. (I'm assuming 192.168.56.101 because that's VirtualBox's default. Make sure it matches the IP for your host-only adapter.)

```bash
# On GUEST: Temporarily assign a static IP to eth1
ifconfig eth1 192.168.56.101 netmask 255.255.255.0 up
```

### Persistent

The last command should work until you have to restart the virtual machine. To make the change persistent, you'll need to modify **/etc/network/interfaces**

```bash
# On GUEST: Modify the configuration file
sudo nano /etc/network/interfaces
```

Add the following to configure eth1 to use a static IP address and come up when the system starts.

```bash
# The host-only network interface
auto eth1
iface eth1 inet static
address 192.168.56.101
netmask 255.255.255.0
network 192.168.56.0
broadcast 192.168.56.255
```

### Accessing the Guest from the Host

Finally, you'll probably want to add some names to your host machine's **/etc/hosts** file. Make sure to add each hostname you will use on your guest.

```bash
# On HOST: edit /etc/hosts
sudo nano /etc/hosts
```

Add a line that starts with the static IP address for the guest, followered by whitespace, then each of the hostnames that should point to your guest.

```bash
# Inside /etc/hosts on your HOST
192.168.56.101 myguest.home.local www.mycoolsite.com anyother.fakesite.com
```

Source: http://christophermaier.name/blog/2010/09/01/host-only-networking-with-virtualbox

From: https://gist.github.com/pjdietz/5768124#file-virtual-box-host-only-static-ip-md
