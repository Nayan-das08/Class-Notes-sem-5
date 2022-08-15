>Chapter - [[EN 2.0 - Cisco IOS and device configuration]]

Aug 3, 2022
Topics - 

# Role of OS
* ***kernel*** - component of OS that interacts with the hardware
- ***shell*** - component which provides interface for user with CLI and GUI

**GUI** can be helpful for easy navigation without managing CLI, but it is not able to provide all the features of CLI. Also, they consume a lot of resources 

**Cisco Internetwork Operating System** is used in many Cisco devices

# Access methods
different methods of configuring network devices

## 1. Console
- provides ***out of band*** service - access via dedicated management channel for maintenance only.
- this port is used to configure a networking device with an end device
- doesn't need active networking services for initial config
- the end device needs terminal emulation software [^1]

## 2. Secure Shell (SSH)
- ***in band*** method for remotely establishing secure CLI connection
- this is done via virtual interface
- requires active interface configured with an address

## 3. Telnet
- ***in band*** method for remotely establishing secure CLI connection
- through a virtual interface
- doesn't provide secure and encrypted connection
- thus used for lab envt.


[^1]: Putty, Tera Team, SecureCRT, used to connect to a networking device (by a console, SSH or Telnet connection), enhances productivity by cosmetic formatting features.