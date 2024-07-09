VLAN (Virtual Local Area Network) - is a virtual network that isolates devices into smaller groups. VLANs are created in the [[LAN]]. Devices in the different VLANs can't communicate between each other on the [[Data link layer]].

VLAN can be configured on [[Switch]] (but not only on that). One Switch can have one or more VLANs and 1 VLAN can be created on one or more Switches.

### Two VLANs in one Switch
Switch has a table of all devices in the network and their [[MAC Address]]'s. More: [[Switch#Data transfer principle]]. In order to distinguish different VLANs, switch also stores`VLAN` field in it's table. Example setup:

| Port Number | VLAN | MAC Address |
| ----------- | ---- | ----------- |
| 1           | 2    | A           |
| 2           | 2    | B           |
| 3           | 10   | C           |
| 4           | 10   | D           |
![[VLAN 1.png]]