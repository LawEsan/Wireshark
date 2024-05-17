# Wireshark | Network Packet Analyser

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53701786467/in/datetaken/" title="Wireshark"><img src="https://live.staticflickr.com/65535/53701786467_1e92afe082_c.jpg" width="800" height="601" alt="Wireshark"/></a>

## Introduction 
In this project I use Wireshark, a tool used to capture and analyse network traffic to intercept and record data packets transmitted between computers on a network as proof of concept that Telnet is not secure. 

Software requirements:
1. Oracle VirtualBox
2. Windows 10 or 11 Enterprise
3. Linux distribution (Ubuntu)
4. Wireshark 
5. Putty

##  Download VirtualBox
- Go to https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html
- Download Windows 64-bit Oracle VM VirtualBox Base Packages - 7.0.14
- Download Oracle VM VirtualBox Extension Pack 7.0.14  7.0.14 ExtPack


<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53695515776/in/dateposted-public/" title="VirtualBox download"><img src="https://live.staticflickr.com/65535/53695515776_534153fcca_c.jpg" width="800" height="409" alt="VirtualBox download"/></a>

## Download Windows 10 ISO Enterprise
- Go to https://www.microsoft.com/en-us/evalcenter/download-windows-10-enterprise
- Download ISO - Enterprise 64-bit edition

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702985780/in/dateposted-public/" title="Download Windows 10 ISO Enterprise"><img src="https://live.staticflickr.com/65535/53702985780_114173a49d_c.jpg" width="800" height="283" alt="Download Windows 10 ISO Enterprise"/></a>

## Download Ubuntu 22.04.4 LTS (Jammy Jellyfish)
- Go to https://www.releases.ubuntu.com/jammy/
- Download 64-bit PC (AMD64) desktop image
  
<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702550856/in/dateposted-public/" title="Ubuntu 22.04"><img src="https://live.staticflickr.com/65535/53702550856_26e3201861_c.jpg" width="800" height="429" alt="Ubuntu 22.04"/>

##  Install Windows 10 ISO Enterprise in Oracle VirtualBox

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702842713/in/dateposted-public/" title="Create Windows-10 VM"><img src="https://live.staticflickr.com/65535/53702842713_005cea6129_c.jpg" width="800" height="445" alt="Create Windows-10 VM"/></a>

- Open Oracle VirtualBox
- Create a new virtual machine by clicking “New”
- Name: Windows-10
- Folder: C:\Users\lesan\VirtualBox VMs
- ISO Image: → Other… → Windows 10 ISO Enterprise
- Click Next
- Base Memory: 2048 MB → Processor: 2 CPUs → Next 
- Disk Size: 50 GB → Next 
- Finish

##  Install Ubuntu in Oracle VirtualBox

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702966399/in/dateposted-public/" title="Ubuntu Install"><img src="https://live.staticflickr.com/65535/53702966399_b8563f7122_c.jpg" width="800" height="552" alt="Ubuntu Install"/></a>

- Create a new virtual machine by clicking “New”
- Name: ubuntu
- Folder: C:\Users\lesan\VirtualBox VMs
- ISO Image: → Other… → Ubuntu 22.04.4 LTS
- Click the box “Skip Unattended Installation” → Next
- Setup account login and make a note of this in Notepad
- Username: bob
- Password: password
- Hostname: Windows-10
- Domain Name: homelab.local
- Base Memory: 2048 MB → Processor: 2 CPUs → Next 
- Disk Size: 25 GB → Next 
- Finish

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53703060670/in/dateposted-public/" title="Win-10 VM setup 2"><img src="https://live.staticflickr.com/65535/53703060670_2f8339abae_c.jpg" width="800" height="446" alt="Win-10 VM setup 2"/></a>

## Configure Ubuntu Network Settings
- In Oracle VirtualBox, click on Ubuntu VM
- Click Settings → Network →  Adapter 2
- Click box “Enable Network Adapter” → Attached to: Internal Network → OK

## Power on Ubuntu VM
- After Ubuntu has finished installing, power on by clicking the start the button.
- Click Try or Install Ubuntu → Install Ubuntu
- Click Minimal Installation 
- Ensure the box “Download updates while installing Ubuntu” is unchecked → Continue
- Click Erase disk and install Ubuntu → Install Now
- Username: bob
- Password: password
- You may see a popup asking if you want to install updated Ubuntu software → Click Remind Me Later
- Connect Your Online Accounts → Skip
- Enable Ubuntu Pro click Skip for now → Next
- No I do need to send system info → Next
- Finish

## Power on Windows-10 VM
- After Windows-10 has finished installing, power on by clicking the start the button.
- Next → Install now → Click “I don’t have a product key
- Select the operating system you want to install → Click Windows 10 ISO Enterprise → Next
- Click the box “I accept the licence terms” → Next
- Custom: Install Windows only (advanced) → Next
- Once it has finished installing, the VM will reboot and ask you to select a region
- Click United States → Yes →  US → Yes → Skip
- Set up for personal use
- Offline account → Limited experience  (if you do not select this, when you will be forced to create a Microsoft account which is unnecessary)
- Setup account login and open Notepad to write login information (so you do not forget)
- Username: red
- Password: password
- Choose privacy settings for your device  → toggle all to No  → Accept
- Once logged in you will you see the following message: Do you want your PC to be discoverable by other pCs and devices on this network? → Click Yes

##  Configure IP address for LAN (Internal) in Ubuntu VM
- In Ubuntu VM, open Terminal app
- Click the network icon in the top right corner of the screen
- You should see Ethernet (enp0s3) Connected and Ethernet (enp0s8) Off
- Ethernet (enp0s3) is the NAT (Network Address Translation) which is associated with the external network, typically the internet
- Ethernet (enp0s8) is the LAN (Local Area Network) connection which is associated with the internal network within your local environment

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702842658/in/dateposted-public/" title="Ubuntu Terminal"><img src="https://live.staticflickr.com/65535/53702842658_d92abbf7fe_c.jpg" width="800" height="551" alt="Ubuntu Terminal"/></a>

- Click on Ethernet (enp0s8) and turn on
- Go back to Ubuntu VM home screen → open Settings → Network
- Click on Ethernet (enp0s8) settings → IPv4
- Click Manual → Assign the following IP address
- Address: 192.168.50.100
- Netmask: 255.255.255.0
- Apply

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702966454/in/dateposted-public/" title="Ubuntu LAN change IP address"><img src="https://live.staticflickr.com/65535/53702966454_9085460e8e_c.jpg" width="800" height="553" alt="Ubuntu LAN change IP address"/></a>


- In the Terminal app, Ethernet (enp0s8) should now appear as connected
- Verify connection is established by typing the command ip a → press enter key
- You should see the IPv4 address you assigned 192.168.50.100

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53703060730/in/dateposted-public/" title="Ubuntu LAN IP has changed"><img src="https://live.staticflickr.com/65535/53703060730_041eb9ba56_c.jpg" width="800" height="552" alt="Ubuntu LAN IP has changed"/></a>

## Configure LAN (Internal) in Windows-10 VM
- Power on Windows-10 VM
- Settings → Network & Internet → Status → Change adapter options
- Here in Network Connections you will see only one connection, which is Ethernet is connected. We need the LAN (internal network) to be connected. To do this shutdown the Windows-VM
- In Oracle VirtualBox, click on Windows-10 Settings
- Network →  Adapter 2
- Click box “Enable Network Adapter” → Attached to: Internal Network → OK
- (Note: The purpose of doing this is to establish an internet connection between both VMs that is needed to communicate with each other for Wireshark to work).
- Restart Windows-10 VM
- Settings → Network & Internet → Status → Change adapter options
- You should now see two network connections, Ethernet & Ethernet 2

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702966384/in/dateposted-public/" title="2 Network Connections"><img src="https://live.staticflickr.com/65535/53702966384_24909a3da2_c.jpg" width="800" height="554" alt="2 Network Connections"/></a>

- Right click Ethernet 2 → Properties → Internet Protocol Version 4 (TCP/IPv4) → Properties → Click Use the following IP address:
- IP address: 192.168.50.50
- Subnet mask: 255.255.255.0
- Click OK
- Close

## Check Internet connection 
- In Windows-10 VM, open Commpand Prompt app
- ping 192.168.50.100
- You should be receiving replies indicating it is working. 
- In Ubuntu VM, open Terminal app
- ping 192.168.50.50
- It is NOT pinging. The reason why it is not pinging is because there is a Firewall that is ON.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702966469/in/dateposted-public/" title="Ubuntu can not ping"><img src="https://live.staticflickr.com/65535/53702966469_a05994b156_c.jpg" width="800" height="590" alt="Ubuntu can not ping"/></a>

- You need to turn the Firewall OFF
- Settings → Windows Security → Firewall & network protection
- Public network (active) → Click to Firewall OFF
- Go back to Terminal app
- ping 192.168.50.50
- It is pinging now, you should be receiving replies indicating it is working. 

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702842708/in/dateposted-public/" title="Ubuntu can ping"><img src="https://live.staticflickr.com/65535/53702842708_4eac252bac_c.jpg" width="800" height="590" alt="Ubuntu can ping"/></a>

## Download Wireshark & Putty to Windows-10 
- In Windows-10 VM → open Microsoft Edge browser
- Go to https://www.wireshark.org/download.html
- Download Windows x64 Installer
- Install

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702892159/in/dateposted-public/" title="Wireshark download"><img src="https://live.staticflickr.com/65535/53702892159_a0d1ba7e90_c.jpg" width="800" height="327" alt="Wireshark download"/></a>

- Go to https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
- Download from Alternative binary files, putty.exe (the SSH and Telnet client itself) 64-bit x86:

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702550841/in/dateposted-public/" title="Putty download"><img src="https://live.staticflickr.com/65535/53702550841_ef17982883_c.jpg" width="800" height="205" alt="Putty download"/></a>

##  Install Telnet on Ubuntu VM via Terminal 
- Open Terminal app
- Type “sudo apt install telnetd” → press the enter key 
- Type your password “password” → press the enter key 
- Do you want to continue? → press y key → press the enter key 
- Telnet is now manually installed
- You can verify it is installed by running this command “sudo dpkg -l | grep telnetd

## Telnet from Windows-10 to Ubuntu VM and capture Wireshark packet analysis

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702626046/in/dateposted-public/" title="Wireshark capture Ethernet 2"><img src="https://live.staticflickr.com/65535/53702626046_8622beaa31_c.jpg" width="800" height="669" alt="Wireshark capture Ethernet 2"/></a>

- In Windows-10, open Wireshark  app
- Click Ethernet 2
- Open putty.exe app
- Click Other → Telnet
- Host Name: 192.168.50.100

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702626136/in/dateposted-public/" title="Putty Configuration"><img src="https://live.staticflickr.com/65535/53702626136_73f2db6e05_o.png" width="448" height="433" alt="Putty Configuration"/></a>

- NOTE: This is your Ubuntu IP address. If you are unsure what this, simply go into your Ubuntu VM, open terminal and run the command ip a
- Click Open (this will Telnet to that IP address and at the same time capture the packet). 
- Login with Username: bob 
- Password: password
- The Windows-10 VM successfully connected to the Ubuntu VM
- Run the command “whoami” and it should return “red”
- Go to Ubuntu VM → open Terminal 
- Run the command “whoami” and it should return “bob”
- Wireshark should be running in the background capturing packets. Click the red square icon to stop the packet capture.
- Type telnet in the search bar and press the enter key to get all the capture data for TCP traffic and telenet traffic
  
<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53702626016/in/dateposted-public/" title="Wireshark Packet Analysis"><img src="https://live.staticflickr.com/65535/53702626016_72b8fb2740_c.jpg" width="800" height="661" alt="Wireshark Packet Analysis"/></a>

- To get the TCP stream → right click on any telnet result → Follow → TCP Stream
- In the TCP Stream, you will be able to see what the user typed. You can see the user’s username is bob, the password the user typed and the last command the user ran in Terminal which was “whoami”. This means you have successfully sniffed the packet. 

<a data-flickr-embed="true" href="https://www.flickr.com/photos/200533061@N05/53703060640/in/dateposted-public/" title="Wireshark TCP Stream"><img src="https://live.staticflickr.com/65535/53703060640_83dc772952_c.jpg" width="673" height="725" alt="Wireshark TCP Stream"/></a>

## Conclusion 
Telnet is a network protocol that allows a user to remotely access and control another computer over the Internet or local area network (LAN). However, its reliance on plain text communication poses inherent security risks. Anyone intercepting the data packets could potentially eavesdrop on the communication between Windows-10 and Ubuntu VM, compromising sensitive information. This project serves as a demonstration of Telnet's insecurity, highlighting the superiority of SSH as a more secure alternative.
