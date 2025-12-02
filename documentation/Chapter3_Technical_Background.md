# CHAPTER III
## TECHNICAL BACKGROUND

This chapter discusses the technical foundations needed to understand how Kamote Korporation's network infrastructure will function. We'll walk through the tools, technologies, and concepts that make modern multi-branch networks possible. Think of this as getting familiar with the building blocks before we actually start constructing anything.

### 3.1 Planning and Documentation Tools

Before diving into the actual network technologies, it's worth mentioning the tools we used to plan and document everything. Good planning tools make the difference between a well-organized project and a chaotic mess.

**Google Docs and Google Sheets**

Google Docs served as our primary collaborative workspace for documenting the project. The beauty of Google Docs lies in its simplicity—you can work on the same document from different locations, leave comments for collaborators, and track every change made along the way (Hanna, 2022). For a project like this where planning and documentation happen iteratively, having everything accessible from anywhere with internet access proved invaluable.

Google Sheets complemented Docs perfectly for organizing the more structured aspects of our planning. When you're dealing with IP address allocation across multiple branches and departments, a spreadsheet becomes essential. Sheets lets you organize network addresses systematically, calculate subnets, and visualize how everything fits together (Chai, 2021). The auto-save feature meant we never had to worry about losing hours of subnet calculations to a computer crash.

**Lucidchart**

For visualizing the network topology, Lucidchart was our go-to diagramming tool. You can't really understand a network by looking at configuration files alone—you need to see it. Lucidchart makes it straightforward to create professional network diagrams, floor plans, and topology maps that actually make sense (Overview of Lucidchart, n.d.). Being able to drag and drop network devices, draw connections, and organize everything visually helped us spot potential issues before they became problems in the actual implementation.

**Cisco Packet Tracer**

Here's where planning meets practice. Cisco Packet Tracer is the simulation software that lets you build and test network configurations without needing actual physical equipment. You can configure routers, switches, and other network devices just like you would in the real world, then see if everything actually works (What is Cisco Packet Tracer, 2020). For a project proposal like this, Packet Tracer provides proof that our design isn't just theoretical—it actually functions as intended.

### 3.2 IP Addressing Fundamentals

Understanding IP addressing is fundamental to any network implementation. Every device that connects to a network needs an address, kind of like how every house needs a street address for mail delivery.

**What is IP Addressing?**

An IP address serves as a unique identifier for each device on a network. Without IP addresses, devices wouldn't know where to send data or how to find each other (Yasar, 2023). Think of it as the foundation of network communication—everything else builds on top of this addressing system.

For Kamote Korporation, proper IP address planning becomes crucial when you're managing multiple branches with different departments. You can't just randomly assign addresses; you need a structured approach that makes sense both now and as the organization grows.

**Classless Inter-Domain Routing (CIDR)**

CIDR revolutionized how we allocate IP addresses. Before CIDR, IP addressing followed rigid class-based rules that wasted huge amounts of address space. CIDR introduced a flexible approach where you can carve up IP address ranges to match your actual needs (Gillis & Burke, 2024).

Instead of being stuck with predefined network sizes, CIDR lets you specify exactly how many addresses you need using a prefix notation. For example, 192.168.1.0/24 tells you that the first 24 bits identify the network, leaving 8 bits for individual devices. This flexibility meant we could allocate just the right amount of address space to each of Kamote Korporation's departments without waste.

**Variable-Length Subnet Mask (VLSM)**

VLSM takes CIDR's flexibility even further. With VLSM, different subnets within the same network can have different sizes (Awati, 2021). This matters tremendously for an organization like Kamote Korporation where departments vary significantly in size.

Consider the main headquarters: the Dispatch Coordination department might need addresses for 20 devices, while Reception might only need 10. VLSM lets us create appropriately sized subnets for each department rather than forcing them all to be the same size. This efficiency in address allocation becomes even more important when you're managing limited address space across multiple branches.

### 3.3 Automatic Network Configuration

**Dynamic Host Configuration Protocol (DHCP)**

Imagine having to manually configure IP addresses for every computer, phone, and device across all of Kamote Korporation's branches. It would be tedious, error-prone, and nearly impossible to manage. That's where DHCP comes in.

DHCP automates the process of assigning IP addresses to devices (Gillis, 2023). When a computer connects to the network, it essentially says "I need an IP address," and the DHCP server responds with "Here you go, use this address, and here's some additional information you'll need." The server handles all the details—IP address, subnet mask, default gateway, DNS servers—automatically.

For Kamote Korporation, DHCP means that when employees arrive at the depot in Mandaue or the pickup point in Lapu-Lapu, they can simply connect their devices and start working. No manual configuration, no calling IT support, no room for human error in entering network settings.

**Domain Name System (DNS)**

DNS solves a fundamental problem: computers work with numbers, but humans work with names. We'd much rather type "inventory.kamotekorp.com" than remember "199.10.5.45" (Lutkevich & Burke, 2021).

DNS acts as the internet's phone book, translating human-friendly names into the IP addresses that computers actually use to communicate. When you type a domain name, DNS servers quickly look up the corresponding IP address and direct your connection to the right place. For Kamote Korporation's internal network, DNS means employees can access the inventory system, quality control database, or dispatch coordination tools using memorable names rather than cryptic numbers.

### 3.4 Network Segmentation and Organization

**Virtual Local Area Network (VLAN)**

VLANs represent one of the most powerful concepts in modern networking. Traditionally, if you wanted to separate different groups on a network, you'd need separate physical switches for each group. VLANs let you create logical separations within the same physical infrastructure (Slattery & Burke, 2022).

For Kamote Korporation, this means we can keep Dispatch Coordination traffic separate from Quality Control traffic, even though they might be on the same floor using the same switches. Each department gets its own VLAN—essentially its own virtual network. This improves both performance (less unnecessary traffic for each device to process) and security (departments can't accidentally interfere with each other's network communications).

Think of VLANs like having different radio frequencies. Everyone might have the same physical radio equipment, but by using different frequencies, different groups can communicate independently without interfering with each other.

**Trunking**

When you have VLANs, you need a way to carry multiple VLAN traffic across the same physical connection between switches. That's what trunking does (Kranz & Burke, 2021). A trunk link can simultaneously carry traffic from many different VLANs, with each data packet tagged to indicate which VLAN it belongs to.

At Kamote Korporation's main headquarters, trunk links connect switches between floors, carrying VLAN traffic for all the different departments through single physical cables. This eliminates the need for separate cables for each VLAN, dramatically simplifying the physical infrastructure.

**EtherChannel**

EtherChannel bundles multiple physical connections between switches into a single logical connection (EtherChannel in computer network, 2023). Why would you want this? Two main reasons: increased bandwidth and redundancy.

If a single link provides 1 Gigabit per second of bandwidth, bundling four links together gives you 4 Gigabits. Plus, if one of those physical links fails, the others keep working—your network keeps running, just with slightly reduced capacity rather than a complete outage. For Kamote Korporation, this redundancy matters tremendously. The main headquarters needs to stay connected to manage operations across all branches, pickup points, and delivery coordination.

### 3.5 Routing: Finding Paths Across Networks

**Understanding Routing Protocols**

Routing protocols are like the GPS of networking—they figure out the best path for data to travel from source to destination. In a multi-branch setup like Kamote Korporation's, routing protocols automatically discover network paths and adapt when something changes.

**Enhanced Interior Gateway Routing Protocol (EIGRP)**

EIGRP is Cisco's proprietary routing protocol, known for being efficient and relatively simple to configure (Sheldon, 2022). It calculates routes based on multiple factors—bandwidth, delay, reliability—and quickly adapts to changes in the network.

For Kamote Korporation's inter-branch communication, EIGRP makes sense. It converges quickly (meaning it adapts fast when something changes), uses bandwidth efficiently, and handles the routing between the main HQ in Cebu, the depots in Mandaue and Lapu-Lapu, and all the pickup points automatically. When we add new locations later—like the planned expansion to Talisay, Consolacion, and Minglanilla—EIGRP will automatically learn about these new networks and incorporate them into its routing decisions.

**Open Shortest Path First (OSPF)**

OSPF is a standards-based routing protocol that uses a different approach than EIGRP. It builds a complete map of the network, then calculates the shortest path to every destination (Awati & Burke, 2023).

For the main headquarters internal routing, OSPF works well. It scales effectively, provides fast convergence, and because it's an open standard, it's well-documented and widely understood. The main HQ's multiple departments and floors create a complex internal network that benefits from OSPF's sophisticated approach to path calculation.

### 3.6 Essential Network Services

**File Transfer Protocol (FTP)**

FTP provides a standardized way to transfer files between computers on a network (Gillis, 2024). For Kamote Korporation, this means quality control reports from the Mandaue depot can be easily sent to the main headquarters, or dispatch coordination can share route optimization files with drivers at different pickup points.

FTP separates into two components: the server (which stores and manages files) and the client (which accesses those files). Employees authenticate with usernames and passwords, ensuring only authorized personnel can access specific files.

**Simple Mail Transfer Protocol (SMTP)**

Email remains a fundamental business communication tool, and SMTP is the protocol that makes email delivery possible (Awati & Gillis, 2024). When you send an email, SMTP handles the behind-the-scenes process of routing that message from your mail server to the recipient's mail server.

For Kamote Korporation's internal communications, having an SMTP server means emails between branches stay within the organization's network rather than routing through external internet mail services. This provides better control, improved security, and faster delivery for internal communications.

**IP Telephony (Voice over IP)**

IP telephony, or VoIP, transforms voice communications from traditional phone lines into data that travels over the network (Doan, 2024). Instead of needing separate phone and data networks, everything runs over the same infrastructure.

For Kamote Korporation, this integration means significant cost savings and operational flexibility. The dispatcher in Cebu can call the quality control supervisor in Mandaue using the same network infrastructure that carries inventory data and email. When a new pickup point opens, adding phone service just means connecting IP phones to the network—no need for separate phone line installation.

IP telephony also enables features that would be expensive or impossible with traditional phones: call forwarding across branches, voicemail to email, presence information showing who's available, and unified communications that integrate voice with other business systems.

### 3.7 Network Security Fundamentals

**Port Security**

Port security controls which devices can connect to switch ports (Aakriti, 2024). By limiting access based on MAC addresses (the unique hardware identifiers burned into network cards), port security prevents unauthorized devices from connecting to the network.

At Kamote Korporation's locations, this means that only approved computers and devices can connect to network ports. If someone tries to plug in an unauthorized device, the port can be automatically disabled, preventing potential security breaches.

**Authentication, Authorization, and Accounting (AAA)**

AAA provides a comprehensive framework for controlling network access (Gillis, 2024b). The three components work together:

- **Authentication**: Verifies who you are (username and password)
- **Authorization**: Determines what you're allowed to do (which resources you can access)
- **Accounting**: Tracks what you actually did (logging for security and auditing)

For Kamote Korporation, AAA means that network administrators can ensure employees only access the systems relevant to their jobs. A driver might access dispatch information but not financial records. An accountant accesses financial systems but not driver routing tools. AAA makes this granular control possible while maintaining detailed logs of who accessed what and when.

### 3.8 Putting It All Together

All these technologies work together to create a functional, secure, and efficient network for Kamote Korporation. The beauty of modern networking lies in how these different pieces complement each other:

VLANs segment the network logically, while DHCP automatically configures devices within those segments. Routing protocols ensure data finds the best path between branches, while IP telephony leverages that same infrastructure for voice communications. Security protocols protect everything, ensuring only authorized access to network resources.

Understanding these technical foundations prepares us for the next chapter, where we'll discuss how we actually implement all these technologies in Kamote Korporation's specific context—the methodology behind turning these concepts into a working multi-branch agricultural logistics network.

---

*This technical background establishes the conceptual and technological framework underlying the proposed network design. The following chapter will detail the specific methodological approaches used to implement these technologies for Kamote Korporation's unique operational requirements.*
