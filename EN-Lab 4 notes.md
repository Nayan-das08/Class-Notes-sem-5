%%[[_Lab Files]]%%
%%#lab/en%% 
%%#incomplete%% 
# Lab 4 
vlan is used to separate/club some FastEthernet ports out of 24 for the same configuration

vlan helps in configuring the switches 

separates the ports (by extn, end devices)

separation of ports can be changed as per requirement

>[!DOUBT]
>**ques**: can one device in vlan 1 communicate with another device in vlan 2
>**ans**: nop

show inter and intra communication

```plain
Switch>enable

Switch#config term

Enter configuration commands, one per line. End with CNTL/Z.

Switch(config)#vlan 10

Switch(config-vlan)#name one

Switch(config-vlan)#vlan 20

Switch(config-vlan)#name two

Switch(config-vlan)#vlan 30

Switch(config-vlan)#name three

Switch(config-vlan)#vlan 40

Switch(config-vlan)#name four

Switch(config-vlan)#vlan 50

Switch(config-vlan)#name five

Switch(config-vlan)#exit

Switch(config)#interface range FastEthernet 0/1-5

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 10

Switch(config-if-range)#interface range FastEthernet 0/6-10

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 20

Switch(config-if-range)#interface range FastEthernet 0/11-15

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 30

Switch(config-if-range)#interface range FastEthernet 0/16-20

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 40

Switch(config-if-range)#interface range FastEthernet 0/21-24

Switch(config-if-range)#switchport mode access

Switch(config-if-range)#switchport access vlan 50

Switch(config-if-range)#exit
```

```plain
C:\>ping 192.168.10.2

Pinging 192.168.10.2 with 32 bytes of data:

Reply from 192.168.10.2: bytes=32 time<1ms TTL=128
Reply from 192.168.10.2: bytes=32 time<1ms TTL=128
Reply from 192.168.10.2: bytes=32 time<1ms TTL=128
Reply from 192.168.10.2: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.10.2:

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
Minimum = 0ms, Maximum = 0ms, Average = 0ms


C:\>ping 192.168.20.1

Pinging 192.168.20.1 with 32 bytes of data:
  
Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.20.1:

Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

![[Pasted image 20220830211319.png]]