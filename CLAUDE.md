# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

This repository contains reference materials and planning documents for a **Networking II Finals Project Proposal**. The project involves designing and simulating a multi-branch network infrastructure for a fictitious company.

### Project Structure

The repository currently contains:
- **INSTRUCTIONS.md**: Guidelines for using this repository as a reference/assistant
- **Reference PDF**: A senior's example project proposal (IP Telephony implementation for a game development company)

### Purpose & Usage

This workspace serves as an **AI-assisted planning environment** for creating a Networking II project proposal. The assistant's role includes:

1. **Analyzing Reference Materials**: Extract patterns, formats, and technical approaches from the example proposal
2. **Drafting Content**: Help write fictitious company profiles, technology descriptions, and network designs
3. **Technical Guidance**: Assist with understanding networking concepts (VLANs, DHCP, routing protocols, IP telephony, etc.)
4. **Packet Tracer Support**: Provide guidance on network topology design and configuration
5. **Educational Support**: Explain systems administration concepts and networking principles

## Key Patterns from Reference Document

### Document Structure (Academic Format)

```
CHAPTER I - INTRODUCTION
- Company background and context
- Business scope and branch locations
- Project objectives

CHAPTER II - REVIEW OF RELATED LITERATURE
- Industry evolution and trends
- Contemporary approaches
- Organizational structures
- Technology implementations

CHAPTER III - TECHNICAL BACKGROUND
- Tools used (Google Docs, Sheets, Lucidchart, Cisco Packet Tracer)
- Networking concepts (IP addressing, CIDR, VLSM, DHCP, DNS, VLANs, etc.)
- Protocols (EIGRP, OSPF, FTP, SMTP, IP Telephony)
- Security measures (Port Security, AAA)

CHAPTER IV - METHODOLOGY
- Structured cabling approach
- IP addressing and subnetting strategy
- Network configuration per branch
- Redundancy and security protocols

CHAPTER V - DISCUSSION AND IMPLEMENTATION
- Detailed implementation explanation
- Network topology diagrams
- Configuration rationale

CHAPTER VI - CONCLUSION AND RECOMMENDATION

APPENDICES
- Floor plans
- Network diagrams
- Configuration codes
```

### Networking Concepts to Understand

**Multi-Branch Network Architecture**:
- Main branch with full departments (Reception, HR, IT, Graphic & Audio, Sales, Marketing, Game Dev, Leisure)
- Satellite branches with reduced departments (IT, Reception, Quality Assurance, Customer Support)
- ISP redundancy (dual providers)

**IP Addressing Strategy**:
- VLSM/CIDR for efficient address allocation
- DHCP for dynamic IP assignment
- Separate VLANs per department
- Management VLAN for network devices
- Voice VLAN for IP telephony

**Redundancy Mechanisms**:
- HSRP (Hot Standby Router Protocol) for router redundancy
- EtherChannel for link aggregation
- Layer 2 redundancy across all branches

**Routing Protocols**:
- OSPF for main branch internal routing
- EIGRP for inter-branch communication
- Route redistribution between protocols

**Security Implementation**:
- Port security on switches
- AAA authentication (RADIUS)
- SSH for remote management
- Access control on console/VTY lines

**Services**:
- DNS server for domain resolution
- FTP for file transfers
- SMTP/POP for email
- IP Telephony (VoIP) for voice communications

### Fictitious Company Profile Pattern

When creating a company profile, include:
- **Company name and industry**
- **Business description and mission**
- **Number and location of branches** (specific addresses)
- **Organizational structure** (departments per branch)
- **Timeline** (when offices will open)
- **Technology needs** (what network services are required)

### Technical Documentation Style

- Use proper academic citations
- Include technical diagrams (floor plans, logical topologies, physical topologies)
- Provide detailed configuration codes in appendices
- Explain WHY each technology choice was made, not just WHAT was implemented
- Use both narrative explanations and visual representations

## Working with This Repository

### Assistant Capabilities

The AI assistant in this workspace can help with:

1. **Company Profile Generation**
   - Create believable fictitious companies
   - Design organizational structures
   - Develop business narratives that justify network requirements

2. **Network Design**
   - Subnet calculations (VLSM/CIDR)
   - VLAN assignment strategies
   - IP addressing schemes
   - Routing protocol selection

3. **Documentation Drafting**
   - Literature review sections
   - Technical background explanations
   - Methodology descriptions
   - Implementation discussions

4. **Cisco Packet Tracer Guidance**
   - Topology design recommendations
   - Configuration command sequences
   - Troubleshooting common issues

5. **Concept Explanations**
   - Networking protocols and their purposes
   - Systems administration principles
   - Best practices for enterprise networks

### Tools Referenced in Example Project

- **Google Docs**: Collaborative document editing
- **Google Sheets**: IP address planning and organization
- **Lucidchart**: Network diagram creation
- **Cisco Packet Tracer**: Network simulation and configuration

### Configuration Patterns

The reference document includes extensive Cisco IOS configurations for:
- Router subinterfaces (router-on-a-stick)
- VLAN trunking and access ports
- EtherChannel port aggregation
- DHCP server pools
- HSRP standby configuration
- IP telephony setup
- AAA/RADIUS authentication
- SSH configuration
- Port security
- Routing protocol (OSPF/EIGRP) setup

## Important Notes

- This is an **educational project** - focus on learning networking concepts
- The assistant should **NOT generate complete solutions** but rather **guide and assist** in creating original work
- Always **understand** the networking concepts being implemented, not just copy configurations
- The goal is to demonstrate comprehension of **multi-branch network design**, **redundancy**, **security**, and **scalability**

## Typical Workflow

1. Analyze reference materials for structure and patterns
2. Develop fictitious company concept and requirements
3. Design network topology and addressing scheme
4. Draft project proposal chapters iteratively
5. Create configuration files for Packet Tracer simulation
6. Generate supporting diagrams and appendices
7. Review and refine complete proposal

## Topology and Implementation Requirements (From telephonyimplementation.pdf)

### PENDING TASK: Packet Tracer Network Design and Configuration

**Status**: Chapters 1-6 complete. Next phase requires topology design, device specification, and Cisco configuration development for Kamote Korporation.

**Network Requirements** (Based on telephonyimplementation.pdf specifications):

#### Main Branch (Kamote Korporation HQ - Cebu City, Banilad)
- **Building**: 3-storey building
- **Departments/Offices**: 8 different departments
  - Reception/Customer Service
  - Administration
  - Dispatch Coordination
  - Inventory Management
  - IT/Network Operations
  - Accounting/Finance
  - Quality Control
  - Driver/Field Staff Support
- **Routers**: 2 (dual ISP - PLDT and Globe)
- **Multilayer Switches (MLS)**: 2
- **Switches**: 7 total
- **Computers**: 5 per office (40 total)
- **IP Phones**: 2 per office (16 total minimum)
- **Routing Protocol**: OSPF (internal)
- **Services**: Website, intranet, email system (FTP, SMTP, HTTP)

#### Branch 1 (Regional Depot - Mandaue City, Talamban)
- **Building**: 1-floor building
- **Offices**: 3 departments
  - Reception
  - Inventory Management
  - Dispatch Coordination
  - Quality Control
- **Routers**: 1
- **Switches**: 2
- **Computers**: 2 per office (6 total)
- **IP Phones**: 1 per office (3 total)
- **ISP Connection**: PLDT

#### Branch 2 (Regional Depot - Lapu-Lapu City, Basak)
- **Building**: 1-floor building
- **Offices**: 3 departments
  - Reception
  - Inventory Management
  - Dispatch Coordination
  - Quality Control
- **Routers**: 1
- **Switches**: 2
- **Computers**: 2 per office (6 total)
- **IP Phones**: 1 per office (3 total)
- **ISP Connection**: GLOBE

#### ISP Configuration Requirements

**ISP (PLDT)**:
- **Routers**: 2
- **Computers**: None (ISP infrastructure only)
- **MultiUser Setup**: 2
- **Routing Protocol**: EIGRP

**ISP (GLOBE)**:
- **Routers**: 2
- **Computers**: None (ISP infrastructure only)
- **MultiUser Setup**: 2
- **Routing Protocol**: EIGRP

### LAN Implementation Requirements

The network MUST implement:

1. **Redundancy**: Multiple paths, EtherChannel, dual ISP
2. **Available and Reliable Networks**: High uptime, failover capabilities
3. **Switching Concepts, VLANs, and InterVLAN Routing**:
   - Separate VLANs per department
   - Voice VLANs for IP telephony
   - Management VLAN
   - Router-on-a-stick or L3 switching for inter-VLAN routing
4. **Layer 2 Security**: Port security, MAC address filtering

### IP Telephony Specific Requirements

- Each office should have minimum 2 IP phones
- Each branch office should have minimum 1 IP phone per office
- Main branch has 2 routers; 1 router connected to PLDT-ISP, 1 router connected to GLOBE-ISP (cloud with 2 routers each)
- IP Telephony system enables communication between departments
- Network design depends on number of offices within each floor
- Minimum 5 computers per office in main branch

### Configuration Tasks Required

When designing topology and configurations, include:

1. **IP Addressing Scheme**:
   - VLSM/CIDR subnetting for all locations
   - Separate subnets for each VLAN
   - Voice VLAN addressing
   - Management VLAN addressing
   - Document in spreadsheet format

2. **VLAN Configuration**:
   - Department VLANs for each location
   - Voice VLANs
   - Management VLAN
   - Trunk configuration between switches

3. **Router Configuration**:
   - Subinterface configuration (router-on-a-stick) if applicable
   - OSPF configuration for Main HQ
   - EIGRP configuration for inter-branch and ISP communication
   - Route redistribution between OSPF and EIGRP
   - DHCP server configuration
   - NAT/PAT for internet access

4. **Switch Configuration**:
   - VLAN creation and assignment
   - Access port configuration
   - Trunk port configuration
   - EtherChannel configuration (link aggregation)
   - Port security implementation
   - VTP configuration (if used)

5. **IP Telephony Configuration**:
   - IP phone setup on voice VLANs
   - Voice VLAN configuration on switches
   - Call Manager Router or dedicated telephony server
   - Inter-branch call routing

6. **Server Services**:
   - DHCP pools for each VLAN
   - DNS server configuration
   - FTP server setup
   - SMTP/Email server
   - HTTP/Web server

7. **Security Implementation**:
   - Port security on access ports
   - AAA configuration (if implementing RADIUS)
   - SSH configuration for remote management
   - Console and VTY line security
   - Access control lists (ACLs) if needed

8. **Redundancy Implementation**:
   - HSRP/VRRP/GLBP for gateway redundancy
   - EtherChannel for switch redundancy
   - Dual ISP routing
   - Backup paths and route selection

### Deliverables for Packet Tracer Implementation

1. **Network Topology File (.pkt)**:
   - Complete Packet Tracer simulation
   - All devices properly configured
   - All connectivity verified and tested

2. **Configuration Files**:
   - Full configuration export for each router
   - Full configuration export for each switch
   - Organized by location and device

3. **IP Addressing Documentation**:
   - Spreadsheet with all subnets
   - VLAN assignments
   - Device IP addresses
   - DHCP pools

4. **Testing Verification**:
   - Screenshots showing successful pings between locations
   - IP phone call tests between branches
   - Routing table verification
   - Redundancy failover tests

5. **Network Diagrams**:
   - Logical topology diagram
   - Physical topology diagram
   - VLAN diagram
   - IP addressing diagram

### Design Approach for Tomorrow's Work

When designing topology:
1. Start with IP addressing scheme (VLSM calculations)
2. Create VLAN assignment table
3. Design logical topology
4. Build physical topology in Packet Tracer
5. Configure devices systematically (ISP → Main routers → Core switches → Access switches → End devices)
6. Test connectivity at each stage
7. Implement redundancy features
8. Configure IP telephony
9. Verify all requirements are met
10. Document everything

## Key Success Factors

- **Coherent narrative**: Company story should justify technical decisions
- **Technical accuracy**: Configurations should be syntactically correct and logically sound
- **Proper documentation**: Follow academic formatting standards
- **Completeness**: Include all required chapters and appendices
- **Originality**: Create unique company scenario and network design

## Changelog Tracking

This repository maintains a **CHANGELOG.md** file to document all modifications, additions, and updates to project materials.

### Changelog Requirements

Whenever making changes to this repository, Claude Code must update the CHANGELOG.md file with:

1. **Date of Change**: Use ISO format (YYYY-MM-DD)
2. **Type of Change**: Categorize as Added, Changed, Modified, Removed, or Fixed
3. **File(s) Affected**: List specific files created or modified
4. **Description of Changes**: Provide clear, concise explanation of what was changed and why
5. **Context**: Include relevant details about scope, approach, or special considerations

### Changelog Format

Follow the [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format:

```markdown
## [Unreleased]

### Added - YYYY-MM-DD
- **filename.ext**: Description of what was added

### Changed - YYYY-MM-DD
- **filename.ext**: Description of what was modified

### Fixed - YYYY-MM-DD
- **filename.ext**: Description of what was corrected
```

### When to Update the Changelog

Update CHANGELOG.md whenever you:
- Create new .md files (chapters, documentation, planning documents)
- Modify existing chapter content
- Add or update diagrams, appendices, or reference materials
- Make significant structural changes to the project
- Create or update configuration files
- Add or modify any substantial content

### Example Changelog Entry

```markdown
### Added - 2025-11-28
- **Chapter3_Technical_Background.md**: Created technical background chapter
  - Covered Cisco Packet Tracer, IP addressing concepts, VLAN theory
  - Included routing protocols (OSPF, EIGRP) explanations
  - Length: Approximately 6 pages in Google Docs format
  - Approach: Technical detail with academic citations
```

This ensures all project evolution is tracked, making it easy to review what changes were made, when, and why.
