DLL (Data link layer) - 2nd layer in [[OSI]] model. It's responsible for sending data between nodes/devices.

DLL receives packets from [[Network layer]] and cuts them into frames. 
![[Data Link Layer 1.png]]
Structure of a frame:
- Ethernet header
	- Destination address ([[MAC Address]])
	- Source address ([[MAC Address]])
	- Type
- Data:
	- IP Header
	- IP Data

> Note: Data is not accurate and shown here just to show that each IP Data is combined with IP Header. It means that if one IP Packet is divided into 20 frames, then IP Header is copied 20 times.

#### References
- https://www.geeksforgeeks.org/data-link-layer/
- https://learningnetwork.cisco.com/s/question/0D53i00000WRWCeCAP/fragmentation-of-ip-packets-into-ethernet-frames-and-defragmentation