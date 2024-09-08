<h1>Active Directoy Home Lab</h1>


<h2>Description</h2>
This project consists of building a Cybersecurity home lab for detection and monitoring. This small-scale Active Directory lab for monitoring and detection walks through configuring, optimizing, and securing an IT infrastructure. Skills and knowledge gained in this lab can be applied to the real-world wether large-scale or small-scale enterprise infrastructure. 
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Bash script</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Splunk</b>
- <b>Pfsense</b>
- <b>Security Onion 2.4</b>
- <b>Kali Linux</b>
- <b>Ubuntu 24.04 desktop</b>
- <b>Ubuntu 22.04 server</b>
- <b>Windows 10 Server</b>

<h2>Project walk-through:</h2>

<p align="center">
Step 1) Home Lab Topology: <br/>
<img src="https://i.imgur.com/CKjyJQz.png"/>
<br />
<br />
Step 2) Creation of pfsense VM and configuration:<br/>
        -Download pfsense community edition ISO
        -Using that ISO create your pfsense VM using these configurations 
<img src="https://i.imgur.com/LOhh7UZ.png"/>
<img src="https://i.imgur.com/5nJXpaa.png"/>
<br />
<br />
Step 3) Creation and configuration of Security Onion server and using Ubuntu 24.04 for accessing the web interface: <br/>
        - Create your SecOnion VM with these configurations and start SecOnion to install and configure it.
<img src="https://i.imgur.com/eGvPxpz.png"/>
        - After installing Security Onion, accessing the web interface will be done from an external Ubuntu VM simulating a SOC analyst SIEM tool.
        - Download the latest Ubuntu desktop ISO once done installing the VM, you go to the terminal and type the command "ifconfig" Once your IP address is shown take note of it. 
        - Here is the Ubuntu VM configuration and also named as SecOnionMgmt
 <img src="https://i.imgur.com/XK6pwMh.png"/>\
        - Switch back to the SecOnion server type the command "sudo so-allow" and type in your Ubuntu VM IP address as we will use this to access SecOnion's web interface.
        
 <img src="https://i.imgur.com/q51d1eS.png"/>\
 <img src="https://i.imgur.com/9C0k9x8.png"/>\
<br />
<br />
Step 4) Using Kali Linux VM to access pfsense web interface:  <br/>
<img src="https://i.imgur.com/4sIlrMH.png"/>
<img src="https://i.imgur.com/1ruacYn.png"/>
        * Click advanced, then accept the risk and continue to logging in to pfsense with the default user and password.
        * Make sure to configure pfsense firewall to allow traffic. 
<img src="https://i.imgur.com/qnAxswP.png"/>
<br />
<br />
Step 5) Creating and configuring Windows 10 desktop and windows 10 server as Domain Controller:  <br/>
~ Important Details for Windows Server Installation
* Install in VMware as usual with defaults
* Do not worry about a product key, simply click Next
* Name the virtual machine the first user you set in your DC
* At the end of the installation, be sure to change the Network Adapter to Vmnet3
* Make sure to UNCHECK “Power on this virtual machine after creation“.
* After the VM has been installed, click “Edit virtual machine settings” and remove the Floppy drive.
* Repeat this process, but this time for the second user.
* Use the same configuration steps as the Domain controller:
* Install, Accept license terms, Use Custom Install
* Once installed make sure to change PC name to designated User.
<img src="https://i.imgur.com/VMymk38.png"/>
<br />
* Navigate to Network Adapter settings
* Right-click on Ethernet0 and select properties
* Select IPV4
* Add an IP Address(192.168.2.21) & Use 192.168.2.1 as the default gateway
* Use 192.168.2.10(VictimsNetwork) as the DNS Server
* Search “domain” and select Access work or school
* Select Connect > Join this device to the local Active Directory Domain
* Enter your domain name.local (monkeydluffy.local)
* Enter the Username: Administrator and the password of your DC
* Select Skip
* Restart
* Repeat this process for the second machine.
* As you can see I've added both virtual machines under active directory users and computers <br />
<br />
<img src="https://i.imgur.com/3Fg0IkL.png"/>
<img src="https://i.imgur.com/l1JxXWr.png"/>
<br />
<br />
Step 6) Installing Splunk on a Ubuntu Server:  <br/>
* For this one instead of using OpenSSH to access Splunk server I just chose to install GUI to the Ubuntu Server as it is easier to navigate.
* Install Ubuntu server ISO 
* Installing the GUI type "sudo apt install Ubuntu-desktop^" 
* After installation reboot the VM using the 'sudo reboot now' command
* on Ubuntu server navigate to splunk.com, download Splunk Enterprise and select the Linux package downloading the .tgz file
* once download is completed, navigate to terminal and 'cd' to downloads folder and 'ls' to comfirm the .tgz file
* Next, you untar the file using the 'sudo tar xvxf <file name>' command.
* navigate to splunk's bin directory. And using the terminal start the splunk instance using this command './ splunk start'
* And now you should be able to access the splunk web interface 'http://splunk:8000'
<img src="https://i.imgur.com/YYNzdFq.png"/>
On your Windows Server, Download the Universal Forwarder
Now install the forwarder:
Accept the License Agreement & click Next
Create a preferred username and password
Enter the IP Address of your Splunk server and the default ports as prompted (8089 & 9997)
Install
Navigate back to your Splunk Instance >> Settings >> Add Data
Select “Forward”
Select the Domain Controller (Windows Server) >> Enter a Server Class Name e.g “Domain Controller” >> Next
Select Local Events Logs and choose your desired event logs >> Next
Select “wineventlog” as the index >> Review >> Submit
This brings us to the end of this homelab. This was fun and exciting to work on and I hope you found value in this process.
<img src="https://i.imgur.com/NiliTLL.png"/>
<img src="https://i.imgur.com/ELycQms.png"/>
<img src="https://i.imgur.com/tBmz0u5.png"/>
<img src="https://i.imgur.com/3Vc8ipm.png"/>
<b>Successful configuration of the Splunk Universal Forwarder</b>
<b>At this point we can work of detection rules or rule tuning. Also we can go back and check the logs from SecOnion at this point.</b>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
