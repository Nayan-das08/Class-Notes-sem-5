>Chapter - [[EN 2.0 - Cisco IOS and device configuration]]

Aug 3, 2022
Topics - [[Cisco IOS MOC]]

# Cisco IOS Command Structure
* set of commands used to administer and configure IOS via CLI
* Each command has specific format


![[Pasted image 20220802094709.png]]

**Keyword** - specific parameters pre-defined in OS
**Argument** - value defined by user (eg. IP address)

---

# IOS Command Syntax Check
| convention | description                             |
| ---------- | --------------------------------------- |
| bold       | cmds or keywords to be entered same     |
| italics    | user args                               |
| [x]        | optional element                        |
| {x}        | required element                        |
| [x{y\|z}]  | required choice within optional element | 

---

# Help Features
2 types - Context sensitive and command syntax check

## context sensitive
* shows help as per the mode currently open
- helps with incomplete finding commands with known starting letters
- shows args and keywords for the cmds

enter a **?** and get help

## command syntax checker
- checks syntax
- shown when incorrect cmd entered in someway
- shown when **?** is not used

---

# Hot Keys

![[Pasted image 20220803000031.png]]

when --More-- is given
![[Pasted image 20220803000144.png]]

To exit
![[Pasted image 20220803000224.png]]

HW - set current system time
