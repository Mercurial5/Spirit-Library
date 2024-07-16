mbuf (Memory buffer) - Block of memory that stores a [[Packet]]. They are stored in [[mempool]]. `mbuf` can store any data, not only packet buffers. But here only packet buffers are considered.

To create an `mbuf`, use `rte_pktmbuf_alloc` method.

## Allocation of an mbuf
Size of an `mbuf` is always fixed and configured on mempool creation. So the number of `mbufs` are always the same. It is important due to how DPDK manages `mbufs`. `mbuf` needs to be created in the heap, since multiple threads can access it at the same time. Memory allocation/deallocation is very expensive operations. And when we are receiving millions of packets, there are millions of allocation/deallocation. In order to resolve this issue, all possible `mbuf` blocks are created in mempool in the beginning. When user needs to create a packet, the `mbuf` will be reserved from mempool and marked that it's not available. After sending a packet, it will again join the mempool as an accessible `mbuf`. Example:

`Mempool` -> `Mbuf initialization` -> `TX Queue` -> `NIC` -> `mempool`

## Structure of an mbuf
![[mbuf 1.png]]
The first block of memory in `rte_mbuf` is data about `mbuf` itself. Then, there is a headroom, user data and tailroom.

### Tailroom
Since the size of an `mbuf` is always fixed, there may be a case when data is too small to fit the whole `mbuf` space. In that case Tailroom will take the remaining space. It's also can be used during modification of an existing packet.

### Headroom
Headroom is configurable at the mempool creation. It's used on a cases, when we need to modify existing packet. For example, add VLAN protocol to it. VLAN comes after Ethernet header, which is located at the start of a user data.

Existing packet:

![[mbuf 2.png]]

Desired packet #1:
![[mbuf 3.png]]

Desired packet #2:
![[mbuf 4.png]]

The difference between #1 and #2, is the direction where we moved the data in our packet in order to fit `VLAN header`. It may be more efficient to move 14 bytes of Ethernet header, than the 1000+ bytes of data. Or there may not be a space in the tailroom. Headroom was created for this purpose.

## Multi-segmented mbuf
When our data is too long to fit [[MTU]], we need to segment our packets. When doing so, it's required to link the packets together so the other end will be able to combine them together into one piece.
![[mbuf 5.png]]
Here we use `next` field in the `rte_mbuf` structure to specify next packet.

## References
- https://doc.dpdk.org/guides/prog_guide/mbuf_lib.html
- https://doc.dpdk.org/api-21.05/rte__mbuf_8h.html#ad4d1c289d8cffc831dfb77c64f52447b