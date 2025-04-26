## Configuring our VMs
Sometimes default settings are okay however there is always a possibility of compromising our host machine whenever we analyze malware in our vm. We gotta reduce the risk as much as possible. 

### Configuring the VMs Network Type
Before we start the configuring the type of network to be used for our vm, we gotta know what these types of network adapters.

1. Default NAT
Each VM will have different networks and will be able to access the internet.

1. NAT network
The VMs will all mesh into one network and can access the internet.

1. Bridged
VMs act as physical machine meaning it'll be on the same network as the host network. Have access to internet and to your LAN. Do NOT execute malware here.

1. Host only network
These VMs are only accessible to the host machine. They won't have access to the internet nor will it have access to your LAN.

1. Internal Network
Goto option when performing malware analysis as this option put the VMs into the same network. You gotta statically assign ip to each VM. Cannot access the internet and your LAN.

1. Not attached

## 2 Scenarios to keep in mind which network adapter to use

1. TESTING TOOLS AND REQUIRE INTERET CONNECTIVITY
Default setting is fine for this. 

1. Analyze malware 
Not have any internet connectivity and be in its own network or not even attaching a network adapter(Not attached). Best option is to use internal network. Allow VMs to communicate with one another and not with the host device. That way we can create a fake internet.   


Windows VM 
IP : 192.168.20.10/24

Linux
Ip : 192.168.20.11/24

```
sudo ip addr add 192.168.20.11/24 dev eth0
```

I ran into a problem with assigning an ip to the linux vm through the GUI but I solved the problem by going into the terminal and manually assigning it there.

## Installing Sysmon

A Microsoft tool that increases your chance at catching malware. Monitor a bunch of events and highly customizable fitting into your environment. Logging mechanism for all the events.

Sysmon Download : https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
Sysmon Config : https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml

Here is the best full tutorial on installing the Sysmon service onto your device.
https://youtu.be/uJ7pv6blyog?si=MuTZ6-gGHsJTu0YN

## Installing Splunk

Splunk is a tool used to view event logs.

Splunk Download : https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us
Splunk config file : https://www.dropbox.com/scl/fi/620i6i0o4idzrtwlqp0qp/inputs.conf?rlkey=elni2v55mpzfab72qxr5wxk3s&e=1&dl=0

Here is the full tutorial.
https://youtu.be/iaBJ-PK8_RI?si=B2nzJ4kPZfYYeXiE

![[Pasted image 20250427000225.png]]
Splunk Login Screen 
Enter your credentials same as the one you used to register at the website.

URI : http://127.0.0.1:8000/en-US/app/launcher/home

