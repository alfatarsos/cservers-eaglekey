<p align="center">
<img width="199" height="200" alt="logoeaglekey-jpg" src="https://github.com/user-attachments/assets/1dd4ff58-3b30-4885-bb00-7419d3d85e23" />
</p>

# C-Servers EagleKey
A turnkey solution for virtualization systems with a simplified approach

# What is it?
A self-hosted virtualization/IaaS platform, based on a dual control server ↔ hypervisor model, with a wealth of features but a strong focus on simplifying technical aspects, and an intuitive and beautiful interface for the client.

It draws inspiration from VirtFusion but moves towards completely different solutions, in a clean-room logic in strict compliance with the software's terms and conditions. Also other inspiration bases exist (e.g., Proxmox, SolusVM 2) for certain functions.

It also implements new quality-of-life functionalities for the client, such as those applicable to automatic NAT management and dashboard management.

# Why the name EagleKey?

Because in a virtual or dedicated hosting market, having a unique platform owned by the company selling the service, changeable and adaptable to existing and future needs, is a key differentiating factor, and allows for a broadly comprehensive service perspective – just like an eagle.

And to be honest, because it was the best name that occurred to the author in the space of 5 minutes that didn't belong to any other brand in the technology sector.

# Will this new platform create disruption for those who have VMs, as happens in migrations between hypervisor products (e.g., SolusVM » VirtFusion, Proxmox » Virtualizor)?

No. The platform will be a drop-in replacement in the structure (crown) immediately outside the covered servers, which will continue to run as normal, and will allow either a clean-slate approach (implementation from scratch) or an in-place conversion approach (potentially introducing small breaking changes that do not affect access to VMs, but may even improve the approach).

It uses QEMU/KVM, and the servers run on QEMU/KVM, which is open-source and usable by everyone; it utilizes networking technologies such as libvirt, MacVTap, which are open-source; it operates in the Linux user-space and kernel-space, which is open-source. Nothing used by commercial products is patentable, except for the (proprietary) recipe, graphics, and implementation method (the so-called IP). As such, users can continue with their services as normal.

# Design Principles
1. Simple — little ceremony, easy to reason and operate.

2. Fast — low latency, low resource consumption.

3. Beautiful — modern and well-designed UI (admin + client).

4. Infinitely replicable — trivial, idempotent deployment on both sides.

5. Reliable — secure, idempotent, and auditable operations on VMs.

# Stack (decided — hybrid model)
• Agent (each KVM host): Go — single binary, native libvirt/nftables.

• Control plane: .NET (ASP.NET Core + Blazor Server) — rich UI and real-time.

• Database: PostgreSQL (import from current MariaDB).

• Contract control↔agent: HTTP/JSON + TLS, JWT RS256 short, OpenAPI spec.

• Cache/queue/realtime: Redis/Valkey. Console: WebSocket → noVNC.

- (NEW) Network statistics extracted directly for easy analysis and abuse monitoring; VictoriaMetrics for other global and private statistics.

- Other elements to be assigned

# Operating Systems for Target in Control Server and Hypervisors.

The primarily supported Linux systems are the same for Control Server and Hypervisors:

» AlmaLinux 10.x (preferred)

» Red Hat Enterprise Linux 10.x

» Rocky Linux 10.x

» SUSE Linux Enterprise Server

» Leap OpenSUSE

» Debian 13

Other Linux systems will not be natively supported as there is no technical or commercial reason to justify it.

Older hypervisor systems, but in the same category, will also not be supported: this tool exclusively uses nftables and never iptables.

The primarily supported Windows operating systems are in Control Server (including Server Core) – a rarity in the industry – and in KVM Virtual Machines:

» Windows Server 2019

» Windows Server 2022

» Windows Server 2026

Hypervisors will support Hyper-V via KVM (global VMs run virtualized on Windows with Enlightenments, based on Linux), a solution that retains on average 100% of the original performance, allows for greater isolation, easier configurations (including extensive SR-IOV possibilities), and better virtualization.

The versioning of these operating systems is stable, enabling inherent stability in the service provided to the customer.

The entire system, from Control Server to Hypervisors, is designed to be as monolithic and enterprise-friendly as possible in its approach.

# Main Functions

- Automatic provisioning of hypervisors and control server via direct script, just like all other similar tooling, but with automatic network configuration (like SolusVM 2)

- Lite Version with loadable text pages, no images, very lightweight and text-based account management, and vi console rsh exposed for VM management. Compatible with GPRS/EDGE/UMTS+ networks, 56K and ISDN phone lines, and pre-Leo/Starlink and similar satellite connections. Allows VM and client account management either in a fixed location, on computers that support browsers like Lynx, or on the go, even on mobile phones with Symbian S60 or Blackberry (via Opera Mini), enabling adaptation to the client's lifestyle anywhere.

- Fast-loading full version, powerful yet simplified in its display, without heavy overlays on the server - up to 10x more performance than commercial control server/hypervisor solutions based on PHP/Laravel, with ASP.NET Core + Blazor/Razor + Go.

- Cross-platform: 1st control system that allows deployment on Windows Server, Linux and BSD provided the correct tooling is supported and installed.

- Automatic user management and in-place migration, with in-VM and real-time controls.

- Easy and accessible interface, even for novices, but without hiding essential information for specialized clients: new interface philosophy on the client side and admin side. Compatible with touch screens and systems.

- Automated systems for controlling business parameters with granularity by plan, user, VM, and dedicated server, with its own hierarchy.

- Automated systems for controlling technical aspects of network volume, CPU usage, and disk usage.

- Fully automatic and highly granular management of CPU, disk, and network abuse.

- Implementation of ballooning options (not implemented by default) for situations where punctual sharing of inter-VM pages or inter-server RAM management is necessary for business or technical reasons and to ensure stability with the client, with granularity by VM, plan, and/or user.

- Native support for 2FA and real-time and <5-second updates of information, status, and business packages, with automatic management.

- Use of Hardware Profiles to place commercial packages in their respective configuration profiles, and automatically provision them in the most efficient way possible according to the tooling required by the hypervisor system, without the need for updates.

- Support for DHCPv4, DHCPv6, Port Isolation, NIC management, SR-IOV, and automatic configuration of v4 and v6 networks without the need to edit files.

- Support for pre- and post-start scripts in a simplified proprietary structure.

- Support for live and semi-live migrations, with almost no downtime, with automatic removal and replacement of NAT IPs.

- Support for High Availability and Latency-Sensitive features in controlled VMs: services maintained by the Client in two or more distinct locations can be replicated for automatic failover and are extremely easy to activate. Ideal for situations where a service simply cannot fail.

- Options for remote storage systems such as S3, NFS, and SFTP, and real-time backup management with system-specific format and automatic encryption.

- Introduction of a two-tiered backup system: customizable "hot backups" in lz4/zstd/gzip, and automatically converted "cold backups" for maximum resource savings by the Provider in lzma2. Decompression is faster than compression.

- Launch of the "Observability" area: a one-stop shop for all inter-dedicated server and inter-VM data.

- Simplification of the Hourly Billing area to simple inter-API communication, virtual hourly management, and accurate fund calculation inspired by SolusVM 2.

- Complementary client management for dedicated servers (via APIs from major manufacturers), clients for semi-dedicated or carry-over (hybrid system), and for containers (container system to be assigned).

- Complementary customer management in Reseller format, a new transaction category, whether through direct sales + mapping of the C-Servers product, or through sales on a dedicated website in WHMCS and Blesta with in-store interaction with the VM by the Client, on VPS/VDS and dedicated servers. Development of an API reseller for prepaid and postpaid systems and for VM communication. The industry's first 360º system with hosting + reselling for virtual and dedicated servers.

- (NEW) Uptime page directly on-platform without any need to use a separate solution, internally and externally (for customers).

- (NEW) Translated in 8 languages: English, Portuguese (Brazil), Portuguese (Portugal), Spanish, French, German, Chinese and Arabic.

- (NEW) Full support for BGP announcements, IP Transit and Tunneling on VPS and Dedicated Servers.

- (NEW) Security measurement for the customer and easy customer onboarding.

- (NEW) Network profiler for automatic provisioning of dual-interface VPS/Server solutions and automatic provisioning/changes on NAT rules and HAProxy, including a new button, "Flush NAT", when a customer gets without NAT access due to conntrack retaining an active connection. 

- Easily replicable across multiple systems to avoid platform downtime for the Client, on all fronts.

# Current Status
Phases 0, 1, 2, 3, 4, 5, 6 and 7 completed; Refinement of communication elements and consideration of other factors underway. Phase 8 in progress. Hardening in progress.

As of June 8, 2026, it is in Beta 2.

Total planned development phases: 9
