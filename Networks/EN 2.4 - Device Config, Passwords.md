>Chapter - [[EN 2.0 - Cisco IOS and device configuration]]

Aug 3, 2022
Topics - [[Cisco IOS MOC]]

>[!NOTE]
>**global config mode** - hostname, set and encrypt passwords, banners
>**privileged EXEC mode** - `show running-config`

# 1 Device Names
each device on a network must have a unique name for identification

## 1.1 Device Name guidelines (for host)
* start with letter
* no spaces, put underscore
* end with letter or number
* number, char or dashes only
* less than 64 chars

you need *global config mode* for changing name as it is is **configuration**

```js
Switch> enable
// enter config mode

Switch(config)# hostname something
//changes the device name

something(config)# no hostname
// sets the default name
```

---

# 2 Password Guidelines
restricting access to administrator modes

## 2.1 key points
* use more than 8 chars
* combination of 
	* upper and lowercase letters
	* numbers
	* special chars
	* numeric sequences

**[[Cisco IOS MOC]] has hierarchical mode of password**

---

# 3 Configure Passwords
## 3.1 setting password for User mode
this is done from console

```js
Switch(config)# line console 0
// enter line console config mode

Switch(config-line)# password some_password
//set password

Switch(config-line)# login
// to enable the password

Switch(config-line)#end
```


## 3.2 setting password for Privileged mode
same method, just change `password` -> `enable secret` (in global config mode)

```js
Switch# configure terminal
// enter global config mode

Switch(config)# enable secret some-other-password
// set the password

Switch(config)# end
// exit
```


## 3.3 setting password for VTY mode
same method as User EXEC mode, just enter `line vty 0 15`

```js
Switch# configure terminal
// enter global config mode

Switch(config)# line vty 0 15
// enter Virtual Terminal line

Switch(config-line)# password vty
// set password

Switch(config-line)# login
// enable the password

Switch(config-line)# end
// exit
```

---

# Password Encryption
we can view the currently entered settings and configurations using `show running-config` in **Privileged mode**

```js
Switch# show running-config
(output left out)
!
!
line con 0
password hello
login
!
line vty 0 4
login
line vty 5 15
login
!
!
!
!
end
```

>[!NOTE] 
Here we can see the passwords are visible to everyone

To encrypt them use `service password-encryption` in global config mode
```js
Switch(config)# service password-encryption
// encrypt the passwords

Switch(config)# end
// exit global config mode

Switch# show running-config
(output left out)
!
!
!
line con 0
password 7 082949420516
login
!
line vty 0 4
login
line vty 5 15
password 7 08375857
login
!
!
!
!
end
```

---

# Banners
To display a message every time we enter, we use **banners**
Set them using `banner motd #message#` in global config mode

```js
Switch(config)#banner motd #Hello there!#
// set the banner message

Switch(config)#end
// exit global config mode
Switch(config)#banner motd #Hello there!#

Switch(config)#end
// exit Privileged Mode


Press RETURN to get started.


Hello there!
// the banner message

User Access Verification

Password:
// entered the password
Switch>
```
