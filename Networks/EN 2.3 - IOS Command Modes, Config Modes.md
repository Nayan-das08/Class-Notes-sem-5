>Chapter - [[EN 2.0 - Cisco IOS and device configuration]]

Aug 3, 2022
Topics - [[Cisco IOS MOC]]

# Command modes
for security, Cisco separates management access into two ***command modes***

## User Mode
- limited capabilities
- useful for basic operations
- limited no of commands for changing config of device
- denoted by `>` symbol
- eg: `Switch>`

## Privileged mode
- used for config commands
- allows access to all commands and features
- used to reach even higher config modes (global config mode)
- denoted by `#` symbol
- eg: `Switch#`

## Conversion
use `enable` for User -> Privileged
use `disable` for Privileged -> User

```plain
Switch> enable
Switch#

Switch# disable
Switch>
```

---

# Configuration mode
- to configure the device, we need ***global config mode***
- from here changes can be made that affect the operation of the device
- denoted by `(config)#` after the device name
- eg: `Switch(config)#`

```plain
Switch# configure terminal
Switch(config)#
// enable mode to global config mode

Switch(config)# exit
Switch#
// global config mode to enable mode
```

we can enter other sub-config modes from here

## Line Config Mode
to configure console, SSH, Telnet, or AUX access
`Switch(config-line)#`

```plain
Switch(config)# line ?

<0-16> First Line number
console Primary terminal line
vty Virtual terminal

Switch(config)#line console 0

Switch(config-line)#

Switch(config-line)#exit

Switch(config)#
```

## Interface Config Mode
to configure a switch port / interface
eg: FastEthernet, Ethernet, etc.
`Switch(config-if)#`

```plain
Switch(config)#interface ?

Ethernet IEEE 802.3
FastEthernet FastEthernet IEEE 802.3
GigabitEthernet GigabitEthernet IEEE 802.3z
Port-channel Ethernet Channel of interfaces
Vlan Catalyst Vlans
range interface range command
```
