# Networking Finals Project - Conversation Summary

**Date**: 2025-12-04

## Overview
This conversation involved configuring a multi-branch network infrastructure for Kamote Korporation with dual ISP connections (PLDT and Globe), HSRP redundancy, IPv4/IPv6 addressing, and OSPF routing.

---

## Tasks Completed

### 1. IPv6 SLAAC Configuration
**File Created**: `dump/ipv6_slaac_commands.txt`

- Configured IPv6 SLAAC (Stateless Address Autoconfiguration) for router subinterfaces
- Enabled `ipv6 unicast-routing` globally
- Configured IPv6 addresses and Router Advertisements for VLANs:
  - VLAN 10: 2001:DB8:B:10::/64
  - VLAN 20: 2001:DB8:B:20::/64
  - VLAN 30: 2001:DB8:B:30::/64
  - VLAN 99: 2001:DB8:B:99::/64
  - VLAN 150: 2001:DB8:B:150::/64
- Used commands: `ipv6 address`, `ipv6 nd prefix`, `no ipv6 nd suppress-ra`

---

### 2. EtherChannel Trunk Fix
**File Created**: `dump/etherchannel_trunk_fix.txt`

**Problem Identified**: Port-channels appeared in `show etherchannel summary` but NOT in `show interfaces trunk`

**Root Cause**: Port-channel interfaces were missing `switchport trunk encapsulation dot1q` command

**Solution**: Added proper encapsulation configuration to all 4 Port-channels:
```
interface Port-channel1
switchport trunk encapsulation dot1q
switchport trunk native vlan 99
switchport trunk allowed vlan 1-1000
switchport mode trunk
```

**Key Learning**: On Cisco Multilayer Switches, trunk encapsulation MUST be set BEFORE switchport mode trunk.

---

### 3. MLS2 Configuration
**File Created**: `dump/mls2_commands.txt`

- Created configuration for second Multilayer Switch (MLS2)
- **Key Difference from MLS1**: NO access ports, only trunk ports and port-channels
- Removed access port configurations (Fa0/1-3)
- Included pre-applied EtherChannel trunk fix
- Configured Gi0/1 as routed port (`no switchport`) for edge router connection
- 4 Port-channels for redundant inter-switch connections
- Same security settings as MLS1 (SSH, passwords, banners)

---

### 4. SVI and HSRP Configuration (IPv4 + IPv6)
**File Created**: `dump/mls_svi_hsrp_ipv4_ipv6_commands.txt`

**IP Addressing Scheme**:

**VLAN 99 Device Assignments**:
- .1 = Virtual IP (HSRP)
- .2 = MLS1 (Primary/Active)
- .3 = MLS2 (Backup/Standby)
- .4 = DHCP/DNS Server
- .5 = HTTP Server
- .6-.12 = 7 Managed Switches
- .13 = Edge Router 1
- .14 = Edge Router 2

**Data VLANs (10, 20, 30, 40, 50, 60, 70, 80, 150)**:
- .1 = Virtual IP (HSRP gateway)
- .2 = MLS1 SVI
- .3 = MLS2 SVI
- .4+ = DHCP pool

**HSRP Configuration**:
- MLS1: Priority 110 (Active)
- MLS2: Priority 100 (Standby)
- HSRPv2 enabled for IPv6 support
- Preempt enabled on both routers
- Virtual IPs configured for both IPv4 and IPv6

**IPv6 Configuration**:
- IPv6 addresses assigned to all SVIs
- IPv6 SLAAC enabled with Router Advertisements
- IPv6 HSRP virtual addresses configured
- Base network: 2001:DB8:A::/48

**IP Helper Configuration**:
- All data VLAN SVIs configured with `ip helper-address 192.168.99.4`
- Points to DHCP/DNS server for DHCP relay

**VLANs Configured**:
- VLAN 10, 20, 30, 40, 50, 60, 70, 80, 99, 150

---

### 5. OSPF Multi-Area Configuration
**File Created**: `dump/ospf_configuration.txt`

**Final Area Design**:

**Area 0 (Backbone)**:
- VLAN 99 (Management)
- VLAN 150 (Voice)
- Rationale: Voice in Area 0 allows reachability to EdgeRouters for telephony DHCP services

**Area 1**:
- VLANs 10, 20, 30, 40
- MLS1 → EdgeRouter1 (PLDT) connection: 192.168.200.0/30
- Primary internet path

**Area 2**:
- VLANs 50, 60
- MLS2 → EdgeRouter2 (Globe) connection: 192.168.201.0/30
- Secondary internet path (metric 10)

**Area 3**:
- VLANs 70, 80

**Key Design Points**:
- MLS1 and MLS2 act as ABRs (Area Border Routers) for all areas
- EdgeRouter1 and EdgeRouter2 act as ASBRs (Autonomous System Boundary Routers)
- Dual ISP redundancy: PLDT primary, Globe backup
- OSPF Router IDs: MLS1=1.1.1.1, MLS2=2.2.2.2, ER1=10.10.10.1, ER2=20.20.20.2
- Default route redistribution configured on both edge routers
- Passive interfaces recommended on end-user VLANs for security

**Configuration Method**: Used `ip ospf 1 area X` on each interface for clean area assignment

---

## Network Topology Summary

```
                    [Internet]
                         |
         +---------------+----------------+
         |                                |
    [ISP PLDT]                       [ISP Globe]
         |                                |
  [EdgeRouter1]                    [EdgeRouter2]
  192.168.200.2                    192.168.201.2
  Area 1 ASBR                      Area 2 ASBR
         |                                |
  192.168.200.1                    192.168.201.1
      [MLS1]                            [MLS2]
   ABR (All Areas)                   ABR (All Areas)
   HSRP Pri 110                      HSRP Pri 100
         |                                |
         +----------[Area 0]--------------+
                (VLANs 99, 150)
                      |
    +-----------------+-----------------+
    |                 |                 |
  Area 1            Area 2            Area 3
(VLANs 10-40)    (VLANs 50-60)     (VLANs 70-80)
```

---

## Key Technologies Implemented

1. **Router-on-a-Stick**: Subinterfaces with 802.1Q encapsulation
2. **HSRP**: Hot Standby Router Protocol for gateway redundancy
3. **OSPF Multi-Area**: 4 areas (0, 1, 2, 3) for logical network separation
4. **EtherChannel**: Link aggregation with LACP (mode active)
5. **Dual-Stack**: IPv4 and IPv6 configured throughout
6. **IPv6 SLAAC**: Stateless autoconfiguration for IPv6 addressing
7. **VLANs**: 802.1Q trunking with native VLAN 99
8. **Dual ISP**: Redundant internet connections with automatic failover

---

## Files Created in /dump

1. `ipv6_slaac_commands.txt` - IPv6 SLAAC configuration
2. `etherchannel_trunk_fix.txt` - Port-channel trunk diagnosis and fix
3. `mls2_commands.txt` - MLS2 full configuration
4. `mls_svi_hsrp_ipv4_ipv6_commands.txt` - SVI, HSRP, IPv4/IPv6 configuration
5. `ospf_configuration.txt` - Multi-area OSPF configuration

---

## Important Notes

### Addressing Scheme Revision
- Initial proposal had data VLANs using .11 for virtual IP, .12/.13 for MLS SVIs
- **Changed to**: .1 for virtual IP, .2/.3 for MLS SVIs (simpler, more standard)

### OSPF Area Design Evolution
- Initially proposed all VLANs in Area 0
- **Revised to**: Logical separation with Area 0 minimal (VLANs 99, 150 only)
- **Further revised to**: Area grouping by VLAN ranges (10-40, 50-60, 70-80)
- **Final design**: Voice VLAN moved to Area 0 for EdgeRouter telephony DHCP access

### Telephony Planning
- Voice VLAN 150 in Area 0 backbone
- EdgeRouters will host telephony DHCP services
- Configuration deferred for future implementation
- IP helper-address on SVIs can point to EdgeRouter IPs via OSPF

---

## Network Specifications

**Main Branch**: Kamote Korporation HQ - Cebu City, Banilad
- 2 Multilayer Switches (MLS1, MLS2)
- 2 Edge Routers (EdgeRouter1, EdgeRouter2)
- 7 Managed Switches
- 10 VLANs (8 data + 1 management + 1 voice)

**ISP Connections**:
- PLDT via EdgeRouter1 (Primary)
- Globe via EdgeRouter2 (Backup, metric 10)

**Inter-MLS Links**:
- 192.168.200.0/30 (MLS1 ↔ EdgeRouter1)
- 192.168.201.0/30 (MLS2 ↔ EdgeRouter2)

**Base Networks**:
- IPv4: 192.168.0.0/16
- IPv6 Main: 2001:DB8:A::/48
- IPv6 Branch: 2001:DB8:B::/48

---

## Verification Commands

**HSRP**:
```
show standby brief
show standby vlan 10
```

**OSPF**:
```
show ip ospf neighbor
show ip route ospf
show ip ospf interface brief
show ip ospf
```

**EtherChannel**:
```
show etherchannel summary
show interfaces trunk
```

**IPv6**:
```
show ipv6 interface brief
show ipv6 route
```

---

## Security Features

- SSH version 2 enabled
- Service password encryption enabled
- Enable secret configured
- Console and VTY line passwords
- VTY 5-15 restricted to SSH with local authentication
- Banner MOTD: "Authorized Personnel Only!"
- Port security on access ports (where applicable)

---

## Next Steps / Future Work

1. Configure telephony DHCP on EdgeRouters
2. Implement IP helper-address for voice VLAN
3. Configure IP phones on VLAN 150
4. Test OSPF convergence and failover
5. Test HSRP failover scenarios
6. Implement QoS for voice traffic
7. Configure NAT/PAT on EdgeRouters for internet access
8. Optional: Implement passive interfaces on SVIs
9. Optional: Configure area range summarization

---

## Lessons Learned

1. **Port-channel encapsulation order matters**: `switchport trunk encapsulation dot1q` MUST come before `switchport mode trunk`
2. **OSPF area design**: Minimal Area 0 is more efficient than putting everything in backbone
3. **Voice VLAN placement**: Placing voice in Area 0 ensures reachability to services across areas
4. **HSRP + OSPF**: Both technologies work independently; HSRP handles gateway redundancy, OSPF handles routing
5. **Dual ISP design**: Use OSPF metrics to control default route preference

---

## Configuration Standards Used

- Router IDs: Sequential (1.1.1.1, 2.2.2.2, etc.)
- OSPF Process: 1
- HSRP Version: 2 (for IPv6 support)
- VLAN 99: Native VLAN on all trunks
- EtherChannel mode: Active (LACP)
- Trunk allowed VLANs: 1-1000

---

## End of Summary
All configurations are copy-pasteable and ready for deployment in Cisco Packet Tracer.
