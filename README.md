# dhcp example

> Configure dnsmasq to assign IP addresses to two virtual machines: bar and baz

## Setup

```
cd dhcp-eample
vagrant up
ansible all -m ping
ansible-playbook dnsmasq.yml
```

Configure interface eth1

Edit `/etc/network/interfaces.d/eth1`:

```
auto eth1
iface eth1 inet dhcp
pre-up sleep 2
```

Stop `ifup@eth1.service`

```
systemctl stop ifup@eth1.service
```

* I haven't succesfully used the `systemctl restart` to set configure an interface

Start `ifup@eth1.service`

```
systemctl start ifup@eth1.service
```

Repeat for machine baz

Ping all machines

```
ansible all -m ping
```

## Links

* https://yulistic.gitlab.io/2018/03/configuring-dnsmasq-only-for-dhcp-server-in-ubuntu-pc/
* https://askubuntu.com/questions/906151/step-by-step-guide-to-setup-a-dhcp-server-client-configuration-in-virtualbox
* https://askubuntu.com/a/967271/382864
* https://www.reddit.com/r/debian/comments/7nw98g/seriously_restarting_network_interfaces/
* https://stackoverflow.com/questions/12538162/setting-a-vms-mac-address-in-vagrant
* https://oss.segetech.com/intra/srv/dnsmasq.conf

## Commands

* `systemctl restart networking.service`
* `systemctl stop ifup@eth1`
* `systemctl start ifup@eth1`
* `ip addr flush eth1`
* `ifconfig`
* `ifup`
* `ifdown`

## Error messages

```
Sep 01 20:39:43 foo dnsmasq-dhcp[4613]: no address range available for DHCP request via eth1
```

Not sure what the root cause was, but I changed my ip range to be in the 192.168.50 network and the error stopped.
