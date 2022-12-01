>Back: [[_Networks]]

# EN 2.0 - Cisco IOS and device configuration

## sub-chapters
```dataview
LIST
FROM [[EN 2.0 - Cisco IOS and device configuration]]
```

## doubts
### 1. what is VTY in global config mode?
used to enable remote access using Telnet or SSH to the device

### 2. What is the difference between `enable password` and `enable secret`

### 3. What is *default gateway*?

### 4. OSI models?

### 5. can't ping using the end-device acting as console to the switch
yes because console connections are dedicated for maintenance only.

### 6. what is `enable secret 5 $...3T91` in `show running-config`?
Privileged EXEC mode password is already encrypted

### 7. Interface?

### 8. no shutdown?

### 9. why configure switch when ping worked earlier?

---
## summary
All end devices and network devices require an operating system (OS). The user can interact with the shell using a command-line interface (CLI) to use a keyboard to run CLI-based network programs, use a keyboard to enter text and text-based commands, and view output on a monitor.

As a security feature, the Cisco IOS software separates management access into the following two command modes: User EXEC Mode and Privileged EXEC Mode.

Global configuration mode is accessed before other specific configuration modes. From global config mode, the user can enter different sub-configuration modes. Each of these modes allows the configuration of a particular part or function of the IOS device. Two common sub-configuration modes include: Line Configuration Mode and Interface Configuration Mode. To move in and out of global configuration mode, use the **configure terminal** privileged EXEC mode command. To return to the privileged EXEC mode, enter the **exit** global config mode command.

Each IOS command has a specific format or syntax and can only be executed in the appropriate mode. The general syntax for a command is the command followed by any appropriate keywords and arguments. The IOS has two forms of help available: context-sensitive help and command syntax check.

The first configuration command on any device should be to give it a unique device name or hostname. Network devices should always have passwords configured to limit administrative access. Cisco IOS can be configured to use hierarchical mode passwords to allow different access privileges to a network device. Configure and encrypt all passwords. Provide a method for declaring that only authorized personnel should attempt to access the device by adding a banner to the device output.

There are two system files that store the device configuration: startup-config and running-config. Running configuration files can be altered if they have not been saved. Configuration files can also be saved and archived to a text document.

IP addresses enable devices to locate one another and establish end-to-end communication on the internet. Each end device on a network must be configured with an IP address. The structure of an IPv4 address is called dotted decimal notation and is represented by four decimal numbers between 0 and 255.

IPv4 address information can be entered into end devices manually, or automatically using Dynamic Host Configuration Protocol (DHCP). In a network, DHCP enables automatic IPv4 address configuration for every end device that is DHCP-enabled. To access the switch remotely, an IP address and a subnet mask must be configured on the SVI. To configure an SVI on a switch, use the **interface vlan 1 global configuration** command. `Vlan 1` is not an actual physical interface but a virtual one.

In the same way that you use commands and utilities to verify a PC host’s network configuration, you also use commands to verify the interfaces and address settings of intermediary devices like switches and routers. The **show ip interface brief** command verifies the condition of the switch interfaces. The **ping** command can be used to test connectivity to another device on the network or a website on the internet.