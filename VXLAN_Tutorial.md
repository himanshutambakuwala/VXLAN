# VXLAN

## What is VXLAN ?



## How does VXLAN work ?

VXLAN provides a way to carry layer 2 (Ethernet) packets over layer3 network. It does so by encapsulating the original layer2 packet into a VXLAN packet.

In VXLAN, a tunnel is formed between VXLAN Tunnel End Points (VTEPs). VTEPs are hosts or network devices that does the VXLAN encapsulation.

VXLAN PACKET:

```
Outer Ethernet Header (VTEP Destination and Source MAC address)
+
Outer IP Header (VTEP Destination and Source IP address)  
+
Outer UDP Header
+
VXLAN Network Identifier (VNI) (24 bit field )
```
