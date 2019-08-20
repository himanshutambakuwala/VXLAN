# VXLAN

## What is VXLAN ?

VXLAN is a tunnelling technology where in the frame is encapsulated with a VXLAN header and transmitted over L3 network.

A switch supporting VXLAN can do following possible actions:
1. Switch the frame to the destination for a locally learnt MAC address.
2. Route the packet as L3 packet.
3. Encapsulate frame in VXLAN and forward to local VTEP.

## How does VXLAN work ?

VXLAN provides a way to carry layer 2 (Ethernet) packets over layer3 network. It does so by encapsulating the original layer2 packet into a VXLAN packet.

In VXLAN, a tunnel is formed between VXLAN Tunnel End Points (VTEPs). VTEPs are hosts or network devices that does the VXLAN encapsulation.

VXLAN PACKET:

```
Outer Ethernet Header (VTEP Destination and Source MAC address) (18 Bytes)
+
Outer IP Header (VTEP Destination and Source IP address) (20 Bytes)
+
Outer UDP Header (8 Bytes)
+
VXLAN Network Identifier (VNI) (24 bit field )
+
Ethernet Frame (to be encapsulated)
```

VXLAN adds 50-54 bytes of overhead with the encapsulation header so the link MTU needs to be configured accordingly.
