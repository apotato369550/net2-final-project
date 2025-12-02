CHAPTER IV
METHODOLOGY

This chapter outlines the systematic approach used to design and develop the multi-branch network infrastructure for Kamote Korporation. The methodology follows a structured planning process that ensures the network meets operational requirements while maintaining scalability, redundancy, and security.

4.1 Design Approach

The network design for Kamote Korporation follows a hierarchical methodology that addresses both current operational needs and future expansion requirements. The design process began with requirements analysis, proceeded through logical and physical design phases, and concluded with implementation planning using network simulation tools.

**Requirements Gathering and Analysis**

The initial phase involved understanding Kamote Korporation's operational structure across all locations. This included mapping departmental communication needs, identifying critical coordination points between branches, and determining the capacity requirements for each facility. The main headquarters in Cebu City, regional depots in Mandaue and Lapu-Lapu, and multiple pickup/drop points each presented distinct requirements that needed to be accommodated within a unified infrastructure design.

**Network Architecture Design**

The architecture follows a hub-and-spoke model that mirrors Kamote Korporation's operational structure. The main headquarters serves as the central hub, with regional depots functioning as secondary hubs for their respective areas, and pickup/drop points connecting as spokes. This hierarchical approach provides efficient resource utilization while maintaining clear communication paths and manageable complexity.

**IP Addressing Strategy**

IP address allocation utilized VLSM principles to efficiently distribute address space across locations and departments. The addressing scheme was designed to support current requirements while reserving capacity for expansion into planned locations including Talisay City, Consolacion, and Minglanilla. Each department received appropriately sized subnets based on device counts and anticipated growth, with careful documentation to prevent addressing conflicts during future expansion.

**VLAN Segmentation**

VLANs were assigned to separate departmental traffic logically across the organization. Each major department—Dispatch Coordination, Inventory Management, Quality Control, Administration, Accounting, and IT Operations—received dedicated VLANs. This segmentation improves both network performance and security by containing broadcast traffic and enabling granular access control policies. A separate management VLAN was designated for network device administration, and voice VLANs were allocated for IP telephony implementation.

**Routing Protocol Selection**

The routing design implements a dual-protocol approach. OSPF handles internal routing within the main headquarters, providing efficient path selection across the multi-floor facility with its eight departments. EIGRP manages inter-branch routing, connecting the main headquarters with regional depots and pickup/drop points. This combination leverages OSPF's strengths for complex internal routing while utilizing EIGRP's efficiency for wide-area connectivity.

**Redundancy Implementation**

Redundancy mechanisms were integrated throughout the design. The main headquarters connects to dual ISPs (PLDT and Globe) to ensure continuous external connectivity. EtherChannel link aggregation provides redundant inter-switch connections, maintaining network operation even if individual links fail. Multiple Layer 3 routing paths ensure traffic can reach destinations through alternate routes if primary paths become unavailable.

**Voice Communication Infrastructure**

IP telephony implementation enables voice communications over the existing data network infrastructure. Each department receives IP phones according to operational requirements—two phones per office in most locations, with adjustments based on departmental size and communication needs. The voice network utilizes dedicated VLANs to ensure quality of service for voice traffic, maintaining call quality even during high data usage periods.

**Security Measures**

Layer 2 security features protect network access at the switch level. Port security restricts which devices can connect to network ports based on MAC addresses. Authentication mechanisms control access to network devices, ensuring only authorized personnel can make configuration changes. Access control lists could be implemented to further restrict traffic flow between VLANs based on organizational security policies.

**Network Services Configuration**

Essential network services support operational requirements across all locations. DHCP servers automate IP address assignment, eliminating manual configuration overhead and reducing configuration errors. DNS services enable name-based resource access rather than requiring users to remember IP addresses. FTP servers facilitate file sharing between branches for operational documents and reports. Email services support internal communications, and web services provide access to organizational resources.

4.2 Simulation and Testing

Cisco Packet Tracer served as the primary simulation environment for design validation. The complete network topology was constructed virtually, including all routers, switches, computers, and IP phones across the main headquarters and branch locations.

**Configuration Development**

Network device configurations were developed systematically, beginning with basic connectivity and progressing through advanced features. Router configurations established IP addressing on interfaces, configured routing protocols, and implemented inter-VLAN routing. Switch configurations created VLANs, assigned ports to appropriate VLANs, configured trunk links, and implemented EtherChannel port aggregation. IP phone configurations integrated voice communications into the network infrastructure.

**Testing Procedures**

Comprehensive testing verified that all design requirements were met. Connectivity testing confirmed that devices within departments could communicate appropriately, inter-department communications functioned according to design, and branch locations could reach the main headquarters and other branches. Routing protocol operation was verified to ensure proper route learning and convergence. IP telephony testing confirmed voice communications functioned across all locations. Redundancy testing validated that backup paths activated when primary links failed.

4.3 Documentation

Throughout the design and simulation process, comprehensive documentation captured all design decisions, addressing schemes, VLAN assignments, configuration files, and testing results. This documentation provides the foundation for eventual physical implementation and serves as reference material for network management and troubleshooting.

The methodology employed ensures that Kamote Korporation's network infrastructure design is systematic, comprehensive, and aligned with operational requirements. The structured approach provides confidence that the design will support current needs while accommodating future organizational growth.

---

*This methodology establishes the systematic process through which Kamote Korporation's network infrastructure was designed and validated. The following chapter presents the detailed implementation and discusses how each component contributes to the organization's communication and connectivity requirements.*
