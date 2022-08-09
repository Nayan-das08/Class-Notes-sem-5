>Chapter - [[EN 2.0 - Cisco IOS and device configuration]]

Aug 7, 2022
Topics - [[Cisco IOS MOC]]

# Config Files
all configs stored in two system files

## startup-config
- stored in NVRAM (Non Volatile RAM)
- contains commands used by device upon startup
- `Switch# show startup-config`

## running-config
- stored in RAM
- shows current configs
- volatile and thus, loses this file on powering off or restarting the device
- `Switch# show running-config`

>[!Save running-config]
>use `copy running-config startup-config` in Privileged EXEC mode

>[!NOTE]
>To remove the changed commands in the running-config, use `reload` in Privileged EXEC Mode
>
>This may cause the network being offline for sometime, resulting in *denial of services*
