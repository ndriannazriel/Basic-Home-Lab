# Basic-Home-Lab

### Pre Requisites
1. VirtualBox
2. Windows ISO file
3. 7zip (Windows device)
4. Kali Pre Built VM
5. Sysmon (Windows device)
6. Splunk (Windows device)

Simply creating vms doesnt mean that there are in a sandbox environment. In other words if you don't configure vm properly, then it can affect your own machine and other machines in your network. YOUR HOST IS TOAST.

Having a Home lab would be able to test out many things and what we will focus for this project is using kali linux to craft your own malware and target the windows machine and try to execute it and see if it logs onto Splunk on the target device.

Always create snapshots before breaking things. Creating a backup is completely necessary so that you can revert back to the snapshot in case something goes wrong.

Lets say you run ransomware and ended up breaking your vm, just restore using the snapshot that you created.





