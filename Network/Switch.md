Switch - is a physical device connected to a network. It allows to transmit data between devices in the current network using [[Data link layer]]. Meaning, it uses [[MAC Address]] to know where to send the data.

Example:
When you send a request to somewhere, you send it to switch, which will transfer it to the [[Router]].

## Data transfer principle
When device is connected to a network, Switch will save the number of port that device was connected to and a MAC Address of the device into a table. Then, when switch receives frames, it will transfer them according to its table:

| Port Number | MAC Address |
| ----------- | ----------- |
| 1           | A           |
| 2           | B           |
| 3           | C           |
| 4           | D           |
![[Switch 1.png]]

> Note: If the MAC Address in frame does not exists in table, it's a [[Unknown Unicast]] frame

> Note: Switch in it's table has another field `VLAN`. More about it can be read in [[VLAN]].

#### References:
- https://en.wikipedia.org/wiki/Network_switch
- http://xgu.ru/wiki/VLAN