# Networking Finals Project - Conversation Summary

**Date**: 2025-12-04 (Updated)

## Project Overview
Multi-branch network infrastructure for **Kamote Korporation** (logistics company) with:
- **Main Branch**: Cebu City, Banilad (8 departments, 2 MLS, 2 EdgeRouters)
- **Branch 1**: Mandaue City, Talamban (3 departments)
- **Branch 2**: Lapu-Lapu City, Basak (3 departments)
- **Dual ISPs**: PLDT (AS 200) and Globe (AS 100)
- **Routing**: OSPF in main branch, EIGRP for inter-branch/ISP communication
- **IP Telephony**: Inter-branch calling system

---

## Recent Session Tasks (Current)

### 1. OSPF Configuration Fixes
**File**: `dump/ospf_configuration.txt`

**Major Changes**:
- **ISP connections moved to Area 0** (from Area 1/2)
- Fixed MLS2 interface from `fa0/1` → `GigabitEthernet0/1`
- Added network statements with wildcard masks
- Added EIGRP redistribution on EdgeRouters
- Removed unsupported Packet Tracer commands (`metric-type`, `always`, `summary-address` in OSPF)

**Final OSPF Area Design**:
- **Area 0**: VLANs 99, 150 + ISP connections (192.168.200.0/30, 192.168.201.0/30)
- **Area 1**: VLANs 10, 20, 30, 40
- **Area 2**: VLANs 50, 60
- **Area 3**: VLANs 70, 80

**EdgeRouter Redistribution**:
- **EdgeRouter1 (PLDT)**: EIGRP AS 200 ↔ OSPF
- **EdgeRouter2 (Globe)**: EIGRP AS 100 ↔ OSPF
- Summary route: `192.168.0.0/16` advertised into EIGRP

---

### 2. EIGRP ISP & Branch Configuration
**File**: `dump/eigrp_isp_branch_config.txt`

**ISP Topology**:
- **PLDT ISP**: AS 200 (2 routers)
  - Router 1 ↔ Main EdgeRouter1: `11.11.11.0/30`
  - Router 1 ↔ Router 2: `15.15.15.0/30`
  - Router 2 ↔ Branch 2: `13.13.13.0/30`
- **Globe ISP**: AS 100 (2 routers)
  - Router 1 ↔ Main EdgeRouter2: `10.10.10.0/30`
  - Router 1 ↔ Router 2: `14.14.14.0/30`
  - Router 2 ↔ Branch 1: `12.12.12.0/30`

**Branch Networks**:
- **Branch 1**: 100.100.x.0/24 (EIGRP AS 100, connected to Globe)
- **Branch 2**: 200.200.x.0/24 (EIGRP AS 200, connected to PLDT)

**Configuration Includes**:
- Full interface configs with IP addresses
- EIGRP network statements with wildcard masks
- Summary routes (100.100.0.0/16, 200.200.0.0/16)
- Interface configs for Main EdgeRouters

---

### 3. IP Telephony Configuration
**File**: `dump/dial_peer_configuration.txt`

**Extension Numbering Plan**:
- **Main Branch**: 1010-1027 (16 phones)
- **Branch 1**: 1110, 1120, 1130 (3 phones)
- **Branch 2**: 1210, 1220, 1230 (3 phones)

**Dial-Peer Patterns**:
- Main: `10[1-2].`
- Branch 1: `11[1-3]0`
- Branch 2: `12[1-3]0`

**Key Configuration Details**:
- **Main EdgeRouter1 (PLDT)**: ONLY telephony server (ip source-address 192.168.150.1)
- **Main EdgeRouter2 (Globe)**: Routes calls only, NO telephony service
- **Branch 1**: Calls route to `10.10.10.1` (EdgeRouter2 WAN IP)
- **Branch 2**: Calls route to `11.11.11.1` (EdgeRouter1 WAN IP)
- **Codec commands removed** (not supported in Packet Tracer)

**Telephony Issues Debugged**:
- Branch phones not receiving numbers → Missing button assignments
- Wrong DHCP option 150 IP
- Session target mismatches (branches pointing to unreachable IPs)
- Main can call branches, but branches can't call main → Fixed by pointing to EdgeRouter WAN IPs

**Current Issue**:
- Branch 2 → Main calls still failing
- EdgeRouter1 telephony service IP mismatch (listening on `192.168.200.2` instead of `192.168.150.1`)
- Need to verify EdgeRouter1 has interface in voice VLAN or can reach it

---

## Network Addressing Scheme

### Main Branch
- **VLANs**: 10, 20, 30, 40, 50, 60, 70, 80, 99, 150
- **Subnetting**: 192.168.x.0/24 (where x = VLAN ID)
- **HSRP Virtual IPs**: .1 (all VLANs)
- **MLS1 IPs**: .2 (all VLANs)
- **MLS2 IPs**: .3 (all VLANs)
- **EdgeRouter Links**:
  - MLS1 ↔ ER1: 192.168.200.0/30
  - MLS2 ↔ ER2: 192.168.201.0/30

### Branch 1 (Mandaue)
- **VLANs**: 10, 30, 40, 70, 99, 150
- **Subnetting**: 100.100.x.0/24
- **ISP Link**: 12.12.12.0/30 (to Globe)

### Branch 2 (Lapu-Lapu)
- **VLANs**: 10, 20, 30, 40, 70, 99, 150
- **Subnetting**: 200.200.x.0/24
- **ISP Link**: 13.13.13.0/30 (to PLDT)

---

## Routing Protocol Architecture

```
Main Branch (OSPF Process 1)
├─ Area 0: Management, Voice, ISP connections
├─ Area 1: VLANs 10-40
├─ Area 2: VLANs 50-60
└─ Area 3: VLANs 70-80

EdgeRouter1 (ASBR): OSPF ↔ EIGRP AS 200
EdgeRouter2 (ASBR): OSPF ↔ EIGRP AS 100

PLDT ISP (EIGRP AS 200)
├─ Router 1 ↔ Router 2
├─ Router 1 ↔ Main EdgeRouter1
└─ Router 2 ↔ Branch 2

Globe ISP (EIGRP AS 100)
├─ Router 1 ↔ Router 2
├─ Router 1 ↔ Main EdgeRouter2
└─ Router 2 ↔ Branch 1

Branch 1: EIGRP AS 100 (matches Globe)
Branch 2: EIGRP AS 200 (matches PLDT)
```

---

## Key Configuration Standards

### OSPF
- **Process ID**: 1
- **Router IDs**: 1.1.1.1 (MLS1), 2.2.2.2 (MLS2), 10.10.10.1 (ER1), 20.20.20.2 (ER2)
- **Configuration Method**: `ip ospf 1 area X` on interfaces
- **Redistribution**: EIGRP routes into OSPF with `subnets` keyword

### EIGRP
- **AS Numbers**: 100 (Globe/Branch1), 200 (PLDT/Branch2)
- **Network Statements**: With wildcard masks
- **Summary Routes**: /16 summaries advertised to ISPs
- **No auto-summary**: Disabled on all routers

### Telephony
- **Voice VLAN**: 150
- **Extension Format**: 4 digits
- **Telephony Server**: EdgeRouter1 only
- **Dial-Peer Protocol**: VoIP
- **Router Model**: 2811 for branches

---

## Packet Tracer Limitations Encountered

1. **OSPF Commands Not Supported**:
   - `metric-type 1` → Removed
   - `default-information originate always` → Changed to `default-information originate`
   - `summary-address` in OSPF → Only works in EIGRP

2. **VoIP Commands Not Supported**:
   - `codec g711ulaw` → Removed (auto-selected)
   - `no vad` → Removed

3. **Interface Naming**:
   - MLS devices use GigabitEthernet, not FastEthernet for uplinks
   - Must use `no switchport` to make MLS interfaces routed

---

## Files Created/Modified

### Configuration Files
1. `dump/ospf_configuration.txt` - Multi-area OSPF with redistribution
2. `dump/eigrp_isp_branch_config.txt` - ISP and branch EIGRP configs
3. `dump/dial_peer_configuration.txt` - Inter-branch telephony dial-peers
4. `dump/telephony_debug.txt` - Telephony troubleshooting config
5. `dump/branch_2_config_dump.txt` - Branch 2 router config
6. `dump/branch_2_telephony.txt` - Branch 2 telephony config

### Addressing Documentation
1. `addressing/IP_Addressing_and_VLAN_Scheme.txt` - Branch addressing
2. `addressing/addressing_for_isp.txt` - ISP link addressing

---

## Troubleshooting Notes

### Telephony Issues
1. **Phones not receiving numbers**:
   - Missing `button 1:x` assignments on ephones
   - Missing `auto assign` and `auto-reg-ephone`

2. **DHCP option 150 wrong**:
   - Should point to router's telephony service IP, not gateway

3. **Inter-branch calling fails**:
   - Session targets must use routable WAN IPs
   - Branches point to EdgeRouter WAN IPs, not internal voice VLAN

4. **Main → Branches works, Branches → Main fails**:
   - Telephony service IP mismatch on EdgeRouter1
   - Need interface in voice VLAN or proper routing

### Routing Issues
- Voice VLANs must be advertised in EIGRP
- Redistribution requires proper metrics in both directions
- Summary routes reduce routing table size

---

## Verification Commands

### EIGRP
```
show ip eigrp neighbors
show ip eigrp topology
show ip route eigrp
show ip protocols
```

### Telephony
```
show telephony-service all
show ephone registered
show dial-peer voice summary
show dialplan number [extension]
debug voip ccapi inout
```

### Connectivity
```
ping [voice-vlan-gateway]
show ip route [voice-network]
traceroute [destination]
```

---

## Next Steps

1. **Fix Branch 2 → Main calling**:
   - Verify EdgeRouter1 has interface in VLAN 150
   - Change telephony-service IP to 192.168.150.1
   - Test end-to-end calling

2. **Complete Network Testing**:
   - Test all inter-branch calls
   - Verify EIGRP route propagation
   - Test ISP failover scenarios
   - Document final topology

3. **Project Deliverables**:
   - Packet Tracer .pkt file
   - Configuration backups
   - Network documentation
   - Testing verification screenshots

---

## Important Reminders

- **Only EdgeRouter1 hosts telephony** - EdgeRouter2 just routes calls
- **Dial-peer numbers don't need to match** between routers
- **Session targets must be routable** via EIGRP/OSPF
- **Voice VLANs in Area 0** for reachability across all areas
- **Summary routes reduce** ISP routing table size
- **EIGRP AS must match** between connected routers

---

## End of Summary
All configurations documented and ready for final testing and deployment.
