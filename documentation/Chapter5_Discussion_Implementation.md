CHAPTER V
DISCUSSION AND IMPLEMENTATION

This chapter discusses the practical implementation of Kamote Korporation's network infrastructure design, explaining how technical concepts translate into a functional multi-branch communication system. The implementation demonstrates how planning and methodology result in operational network capabilities that support the organization's agricultural logistics operations.

5.1 Network Infrastructure Overview

The implemented network infrastructure creates a unified communication platform connecting Kamote Korporation's main headquarters in Cebu City with regional depots in Mandaue and Lapu-Lapu, as well as multiple pickup/drop points across the service area. The design accommodates current operational requirements while providing the scalability necessary for planned expansion into additional municipalities.

**Hierarchical Network Design**

The implementation follows a three-tier hierarchical model adapted to Kamote Korporation's organizational structure. The core tier, located at the main headquarters, provides high-speed backbone connectivity and inter-VLAN routing capabilities. The distribution tier, represented by regional depot networks, aggregates connections from local departments and facilitates communication with the core. The access tier, including switches at all locations, provides direct connectivity for end-user devices including computers, IP phones, and other network-enabled equipment.

**Main Headquarters Implementation**

The main headquarters network supports eight departments across a multi-floor facility. Each department operates within dedicated VLANs, with inter-VLAN routing provided by Layer 3 switches or router-on-a-stick configuration depending on equipment capabilities. The headquarters hosts critical network services including DHCP servers, DNS servers, FTP file sharing, email services, and IP telephony call managers. Redundant routers provide dual ISP connectivity to both PLDT and Globe, ensuring continuous external communications.

**Regional Depot Networks**

The Mandaue and Lapu-Lapu depot networks implement scaled versions of the headquarters design, supporting their respective departments with VLAN segmentation and local network services. Each depot maintains local DHCP services for automatic device configuration and connects to the main headquarters through dedicated WAN links. Routing protocols ensure that inter-branch communications follow optimal paths while maintaining alternate routes for redundancy.

**Pickup/Drop Point Connectivity**

Smaller pickup/drop points implement simplified network configurations appropriate to their operational scope. These locations connect to the nearest regional depot or directly to the main headquarters, depending on geographical and operational considerations. Even at these smaller locations, IP telephony enables seamless voice communications with all other organizational facilities.

5.2 IP Addressing and VLAN Implementation

The IP addressing scheme organizes network resources logically, with address ranges allocated to support current needs and future expansion. VLSM techniques ensure efficient address utilization, with subnet sizes matched to departmental device counts. Documentation of address assignments prevents conflicts and facilitates troubleshooting.

VLAN implementation segments network traffic according to organizational structure and functional requirements. Departmental VLANs separate traffic by business function, management VLANs isolate network device administration, and voice VLANs prioritize IP telephony communications. Trunk links between switches carry multiple VLANs simultaneously, with proper tagging ensuring traffic reaches intended destinations.

5.3 Routing Protocol Configuration

OSPF configuration within the main headquarters creates a dynamic routing environment that adapts to topology changes. Routers and Layer 3 switches exchange routing information, building complete network maps and calculating optimal paths to all destinations. The protocol's fast convergence ensures minimal disruption if network links fail or topology changes occur.

EIGRP configuration manages inter-branch routing, connecting geographically dispersed locations through the ISP networks. Route redistribution between OSPF and EIGRP at boundary points ensures seamless communication between headquarters internal networks and branch locations. The dual-protocol approach optimizes routing for different network segments while maintaining organizational connectivity.

5.4 Redundancy and High Availability

Multiple redundancy mechanisms ensure network reliability. Dual ISP connections provide external connectivity redundancy—if the PLDT connection fails, traffic automatically routes through Globe, and vice versa. EtherChannel link aggregation bundles multiple physical connections between switches, providing both increased bandwidth and automatic failover if individual links fail. Multiple routing paths ensure that traffic can reach destinations through alternate routes if primary paths become unavailable.

5.5 IP Telephony Deployment

IP telephony implementation replaces traditional phone systems with voice-over-IP communications. IP phones connect to network switches configured with voice VLANs, ensuring quality of service for voice traffic. Call manager servers at the main headquarters coordinate call routing, voicemail services, and advanced features. Inter-branch calls traverse the same network infrastructure that carries data traffic, eliminating separate phone line expenses while providing superior functionality.

Each office location receives IP phones according to operational requirements. The main headquarters departments receive two phones per office, ensuring adequate communication capacity. Branch locations and pickup/drop points receive appropriate phone allocations based on their operational scope and staff counts.

5.6 Network Services Integration

DHCP services automate IP address assignment across all locations. Servers at the main headquarters and regional depots provide address pools for their respective locations, eliminating manual device configuration and reducing errors. DNS services enable name-based resource access, allowing employees to access network resources using intuitive names rather than numeric IP addresses.

File transfer capabilities via FTP support operational workflows requiring document and data sharing between locations. Quality control reports, dispatch schedules, inventory records, and other operational data can be efficiently transferred between facilities. Email services facilitate internal communications, with SMTP servers handling message delivery across the organization.

5.7 Security Implementation

Layer 2 security features protect network access. Port security on switches prevents unauthorized devices from connecting to the network by restricting access based on MAC addresses. If an unknown device attempts to connect, the switch port can be automatically disabled, preventing potential security breaches.

Access control to network devices themselves prevents unauthorized configuration changes. Console and VTY line access requires authentication, ensuring only authorized IT personnel can modify network settings. Different privilege levels could be implemented to provide appropriate access for different administrative roles.

5.8 Testing and Validation

Comprehensive testing validated all aspects of the implementation. Connectivity tests confirmed that devices could communicate within their VLANs, across VLANs when appropriate, and between locations. Routing protocol operation was verified by examining routing tables and observing how routes change when links fail. IP telephony testing confirmed voice quality and call completion rates across all locations.

Redundancy testing deliberately failed primary links and connections to verify that backup mechanisms activated properly. These tests demonstrated that the network maintains operation even when individual components fail, providing the reliability necessary for business-critical communications.

5.9 Operational Benefits

The implemented infrastructure addresses the operational challenges identified in Chapter I. Unified voice communications eliminate the fragmentation of personal mobile devices and disparate communication channels. Real-time coordination between dispatch, inventory management, and quality control departments improves operational efficiency. Cost management benefits accrue from eliminating per-location telecommunications service contracts in favor of organizational infrastructure. Scalability is built into the design, enabling new locations to be added without fundamental architectural changes.

The network infrastructure becomes an operational asset that enables better business processes rather than simply providing basic connectivity. The integration of voice, data, and network services creates a platform that supports current operations while enabling future capabilities as the organization evolves.

---

*This implementation discussion demonstrates how network design principles translate into functional infrastructure supporting Kamote Korporation's operational requirements. The following chapter concludes the proposal and provides recommendations for moving forward with physical implementation.*
