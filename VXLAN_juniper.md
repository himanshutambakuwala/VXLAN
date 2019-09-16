# Configuring VXLAN on Juniper devices

For VXLAN to work, below parameters is required:
1. The VTEP source interface on each TOR. This will be the source address on the packets. This needs to be configured.
2. The VTEP destination addresses on each TOR. This will be the source address on the packets. This can be statically configured or dynamically learned via protocols.
3. The VNI address.


## QFX as leaf

### Basic configuration

Define the source interface for VTEP:
```
leaf1# show switch-options
vtep-source-interface lo0.0;
```
Create VXLAN enabled VLAN:
```
leaf1# show vlans
VLAN100 {
    vlan-id 100;
    vxlan {
        vni 100;
        encapsulate-inner-vlan;
    }
}
```
Configure server facing interface:
```
leaf1> show configuration interfaces xe-0/0/2
unit 0 {
    family ethernet-switching {
        interface-mode trunk;
        vlan {
            members VLAN100;
        }
    }
}
```
For destination VTEP address, 
1. Static method:
```
set switch-options remote-vtep-list 1.1.3.2;
```
```
set vlans VLAN100 vxlan ingress-node-replication
```
2. Multicast learning:
```
set protocols pim rp static address 1.1.1.1
set protocols pim interface lo0.0;
set protocols pim interface all;
```
```
set vlans VLAN100 vxlan multicast-group 233.252.0.2
```
The RP can be spine or gateway device in the network. Tunnel services may be required for this method to work.
3. BGP EVPN:
```
set switch-options route-distinguisher 1.1.3.1:100
set switch-options vrf-target target:1:100
```
```
set vlans VLAN100 vxlan ingress-node-replication
```
```
set protocols evpn vni-options vni 100 vrf-target target:1:100
set protocols evpn encapsulation vxlan
set protocols evpn multicast-mode ingress-replication
set protocols evpn extended-vni-list 100
```
IBGP peering between leaf to exchange the VTEP information:
```
set protocols bgp group EVPN_VXLAN_LEAF type internal
set protocols bgp group EVPN_VXLAN_LEAF local-address 1.1.3.1
set protocols bgp group EVPN_VXLAN_LEAF family evpn signaling
set protocols bgp group EVPN_VXLAN_LEAF neighbor 1.1.3.2
set protocols bgp group EVPN_VXLAN_LEAF neighbor 1.1.3.3
```
If the VTEP information is required to be sent across data centers, e-BGP peering needs to be configured on leaf with local gateway:
```
set protocols bgp group EVPN_VXLAN_CORE type external
set protocols bgp group EVPN_VXLAN_CORE multihop ttl 255
set protocols bgp group EVPN_VXLAN_CORE multihop no-nexthop-change
set protocols bgp group EVPN_VXLAN_CORE local-address 1.1.3.1
set protocols bgp group EVPN_VXLAN_CORE family evpn signaling
set protocols bgp group EVPN_VXLAN_CORE peer-as 65403
set protocols bgp group EVPN_VXLAN_CORE local-as 65400
set protocols bgp group EVPN_VXLAN_CORE neighbor 1.1.1.1
```


Operational commands:
To verify the VTEP source configuration:
```
show ethernet-switching vxlan-tunnel-end-point source
```
To verify the VTEP destination configuration/learning:
```
show ethernet-switching vxlan-tunnel-end-point remote
```
To check the VTEP learning in VXLAN:
```
show route table :vxlan.inet.0
```
To verify the mac-addresses learnt and the VTEP interface mapped to mac:
```
show ethernet-switching table
```
