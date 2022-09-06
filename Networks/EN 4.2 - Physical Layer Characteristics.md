>Chapter - [[EN 4.0 - Physical Layer]]

Sep 6, 2022
Topics - 

# Standards for Physical Layer
1. ISO - *International Organization for Standardization*
2. TIA/EIA
3. ITU-T
4. ANSI - *American National Standards Institute*
5. IEEE

## the standards address three areas
1. Physical Components
2. Encoding
3. Signaling

---
# physical components
hardware devices that transmit the signals representing the bits on the channel

---
# encoding
- converting the stream of bits into a form that is recognised by the next device
- method to represent digital information
- methods: 
	- Manchester algorithm
		- 0 bit - high to low voltage transition
		- 1 bit - low to high voltage transition
		- used in older Ethernet standards (10BASE)
	- 4B/5B
		- used in Ethernet 100BASE-TX
	- 8B/10B
		- used in Ethernet 1000BASE-T

---
# signalling
- how bits are represented in the media
- examples -
	- change in intensity of light
	- voltage
	- duration of pulse (like in Morse Code)
	- amplitude, frequency or phase modulation (AM, FM, PM)

---
# bandwidth
- amount of data that can flow through a channel in a given amount of time
- units - bps and so on

## latency 
some delay for data transmission

## throughput
measure of bits transferred over a given period time

## goodput
throughput - traffic overhead (latency)
usable data transferred over a given period of time

>[!NOTE]
>goodput < throughput < bandwidth
