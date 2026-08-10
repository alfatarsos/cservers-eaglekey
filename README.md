<p align="center"><img width="180" height="180" alt="eaglekey-180" src="https://github.com/user-attachments/assets/ce4d9faa-26cd-4c81-a0d5-73e4fe180d68" /> </p>

# C-Servers EagleKey
A turnkey solution for virtualization systems with a simplified approach

# What is it?
A self-hosted virtualization/IaaS platform, based on a dual control server ↔ hypervisor model, with a wealth of features but a strong focus on simplifying technical aspects, and an intuitive and beautiful interface for the client.

<p align="center">
<img width="840" height="525" alt="eg8" src="https://github.com/user-attachments/assets/2fc54c81-4162-4fdb-97c8-d171d681807a" />
</p>

<p align="center">
<img width="840" height="525" alt="eg5" src="https://github.com/user-attachments/assets/d30ce6e4-76f0-4190-a15b-5f732dc69db8" />
</p>

It draws inspiration from VirtFusion but moves towards completely different solutions, in a clean-room logic in strict compliance with the software's terms and conditions. Also other inspiration bases exist (e.g., Proxmox, SolusVM 2) for certain functions.

It also implements new quality-of-life functionalities for the client, such as those applicable to automatic NAT management and dashboard management.

<p align="center">
<img width="840" height="525" alt="eg6" src="https://github.com/user-attachments/assets/be2aa2dd-43ae-4997-aa93-bcd888c4e04a" />
</p>

<p align="center">
<img width="840" height="525" alt="eg4" src="https://github.com/user-attachments/assets/99489a67-4c86-4d3d-b71f-f2fbd5cd2db6" />
</p>

# Why the name EagleKey?

Because in a virtual or dedicated hosting market, having a unique platform owned by the company selling the service, changeable and adaptable to existing and future needs, is a key differentiating factor, and allows for a broadly comprehensive service perspective – just like an eagle.

And to be honest, because it was the best name that occurred to the author in the space of 5 minutes that didn't belong to any other brand in the technology sector.

# Will this new platform create disruption for those who have VMs, as happens in migrations between hypervisor products?

No. The platform is a drop-in replacement in the structure (crown) immediately outside the covered servers, which will continue to run as normal, and will allow a clean-slate approach (implementation from scratch) and an in-place conversion approach with merely 15 seconds of downtime.

It uses Cloud Hypervisor and QEMU/KVM, and the servers run on these, which are open-source and usable by everyone; it utilizes networking technologies such as libvirt, MacVTap, which are open-source; it operates in the Linux user-space and kernel-space, which is open-source. Nothing open-source used by commercial products is patentable, except for the (proprietary) recipe, graphics, and implementation method (the so-called IP). Neither of those are used here, as observable with the images.

# Design Principles
1. Simple — little ceremony, easy to reason and operate.

2. Fast — low latency, low resource consumption.

3. Beautiful — modern and well-designed UI (admin + client).

4. Infinitely replicable — trivial, idempotent deployment on both sides.

5. Reliable — secure, idempotent, and auditable operations on VMs.

# Stack (decided — hybrid model)
• Agent (each KVM host): Go — single binary in Go, native libvirt/nftables and communication to the Control plane.

• Control plane: .NET (ASP.NET Core + Blazor Server) — rich UI and real-time; Kestrel and Nginx. Up to 10x more performance than similar PHP-based solutions, with continuous maintenance guaranteed on both stacks: Go and .NET retain code compatibility and reasoning throughout versons for many years.

• Database: PostgreSQL.

• Console: WebSocket → noVNC, Serial Console.

• VictoriaMetrics for other global and private statistics and general uptime verification, public and private.

# Target Operating Systems

The primarily supported Linux systems are the same for Control Server and Hypervisors:

» AlmaLinux 10.x (preferred) / RHEL 10 (preferred) / Rocky Linux 10 / Oracle Linux 10

» Debian 13.x 

» openSUSE Leap 16.0 / SLES 16 (minimum .NET 10 LTS on control; hypervisor demands ndppd on Zypper; versioning mandatorily EL10-synced)

Older hypervisor systems or systems that do not implement nftables by default are not supported: this tool exclusively uses nftables and never iptables.

The entire system, from Control Server to Hypervisors, is designed to be as monolithic and enterprise-friendly as possible in its approach. The versioning of these operating systems is stable, enabling inherent stability in the service provided to the customer.

# EagleKey Functions

- Automatic provisioning of hypervisors and VMs via GUI and billing modules, just like all other similar tooling, but with automatic network configuration (like SolusVM 2) and a fallback manual scripting tool.

- Lite Version with loadable text pages, no images, very lightweight and text-based account management, with console included. Compatible with GPRS/EDGE/UMTS+ networks, 56K and ISDN phone lines, and pre-Leo/Starlink and similar satellite connections. Allows VM and client account management either in a fixed location, on computers that support browsers like Lynx, or on the go, even on mobile phones with Symbian S60 or Blackberry (via Opera Mini), enabling adaptation to the client's lifestyle anywhere. 

- Up to 10x more performance than commercial control server/hypervisor solutions based on PHP/Laravel - EagleKey implements .NET Core 10 LTS + Blazor/Razor + Go and does not implement Javascript.

. Automatic user management and in-place migration, with in-VM and real-time controls. 2FA, magic links and normal logins directly implemented. Native support for real-time updates of information, status, and business packages.

- Easy and accessible interface, even for novices, but without hiding essential information for specialized clients: new interface philosophy on the client side and admin side, clean and direct. Compatible with touch screens.

- Automated systems for controlling business parameters with granularity by plan, user, VM, and dedicated server, with its own hierarchy; and for controlling technical aspects of network volume, CPU usage, RAM usage and disk usage, automatically and without any intervention needed. This will contribute for added performance for our customers, while resource abuses will be correctly and automatically held by the system with no administrative intervention required.

- We introduce Hardware Profiles in a different approach as to other panels, in order to place commercial packages directly in their respective configuration profiles, and automatically provision them in the most efficient way possible according to the tooling required by the hypervisor system, without any need for updates. Pre-compatible with the highest versioning from our virtualization platforms.

- For the first time at C-Servers: Cloud Hypervisor (CHV/KVM) with microVM and Direct Linux Booting (no UEFI/BIOS) is implemented with KVM on major Linux distributions. Advantages include 200ms booting, significant RAM savings for the user and the provider, performance increases and lower usage latency, all while retaining full KVM functionality. A Debian 13 distribution has reportedly reduced from 220MB to only 85MB on-system without forfeiting systemd, OpenSSH or essential packages. This is all provided by Cloud Hypervisor but also our own optimization measures. 

- Legacy VirtFusion usersstay automatically at QEMU/KVM on their original install without any intervention needed, until they choose to reinstall any operating system. However, it is very much recommended for existing customers to reinstall their systems, because of the added performance and RAM savings.

- Automated testing, failover and if necessary rollback of OS reinstall attempts.

- Support for legacy systems pre-2004 built-in via QEMU/KVM: a relevant but unexplored use-case for virtualization for companies and customers. 

- Networking support for DHCPv4, DHCPv6, Port Isolation, automatic NIC management, SR-IOV, and automatic configuration of v4 and v6 networks without the need to edit any files, in Libvirt NAT and MacVTap, and semi-automatic in Linux Bridges; pre- and post-start scripts are compatible in a simplified structure under Provisioners. Cloud-init by default configured on all distributions (inspired on SolusVM 2).

- Network profiler for automatic provisioning of dual-interface VPS/Server solutions and automatic provisioning/changes on NAT rules and HAProxy. This includes a new button, "Flush NAT", when a customer gets without NAT access due to conntrack retaining an active connection - a previous bug detected on VirtFusion we're addressing on this new panel following user feedback.

- Direct support for live and semi-live migrations, with almost no downtime (15 + 15 seconds), with automatic management of IPs and removal + replacement of NAT IPs. The time of having 5-10 minutes of downtime due to server migrations is over.

- Semi-direct support for High Availability (CEPH/DRBD) and Latency-Sensitive features in controlled VMs: services maintained by the Client in two or more distinct locations can be replicated for automatic failover (internal feature). 

- Dataset ptions for local (RAW and LVM Thin) and remote (CEPH and NFS) storage systems, and real-time backup management with system-specific format (.ekbak) and deployment through zstd and restic dedup + automatic encryption, separated between QEMU-based VMs and CHV-based VMs automatically and without any manual intervention required.

- Launch of the "Observability" area: a one-stop shop for all inter-dedicated server and inter-VM data. Routed network abuse pattern tracking identification on "Traffic Flows", with potential abuse and clear abuse patterns communicated to admins every 12h at rolling times and easy, low-cost processing of such data with 7-day abuse pattern information retention, for easy management.

- Simplification of the Hourly Billing area to simple inter-API communication: directly thought for resellers, hourly servers and dedicated servers with virtual hourly management, and accurate fund calculation.

- For the first time at C-Servers, dedicated server management is now directly supported on a Server Management Platform: we implement Redfish and general IPMI/API communication on pre-Redfish servers via API from major manufacturers, including Dell, HP and Supermicro. Autonomous client management will be available in dedicated and semi-dedicated servers.

- For the first time at C-Servers, dedicated customer management in Reseller format is now supported, a new transaction category, whether through direct sales + mapping of the C-Servers product, or through sales on a dedicated website in provided modules for WHMCS and Blesta with in-store interaction with the VM by the Client, on VPS/VDS and dedicated servers. Development of a direct API reseller for prepaid and postpaid systems and for VM communication. One of the industry's first 360º systems with hosting + reselling for virtual + dedicated.

- Uptime page (in English) directly on-platform without any need to use a separate solution, internally and externally (for customers). Network Status page directly integrated into Uptime with automatic downtime warnings/resolution to accelerate problem-solving, but also supporting manual text, continuous updates from PC and mobile, and, at the end of each issue, an optional Provider Technical Report that details the issues taken and the action taken. 

- EagleKey is translated in 8 languages: English, Portuguese (Brazil), Portuguese (Portugal), Spanish, French, German, Chinese and Arabic.

- Full support for BGP announcements, IP Transit and Tunneling on VPS and Dedicated Servers.

- Security measurement for the customer and easy customer onboarding with a 3-step process.

- Easily replicable across multiple systems via Nginx and PostgreSQL to avoid platform downtime for the Client, on all fronts.

# Current Status, Development Tools and Versioning
Launched in-production as of June 27th, 2026, at version 1.3.0 (agent + control), and declared Stable. 

As of 10-08-2026, EagleKey has a redesigned logo and it's now at version 3.1.0 (agent + control), declared Stable.

Total rounds of security hardening completed: 21, including pentests, code inspection and multiple fixing rounds. Total number of counted operational functions: 200+. Parity with VirtFusion-counted functions: 85%.

Development Tools: Claude Fable 5 / Opus 4.8 / Sonnet 4.6 (45%); Cursor Composer 2.5 (25%); ChatGPT 5.6 Sol + Luna / 5.5 / Codex 5.3 (30%). Total lines: 160.000 (Control + Agent).

Total development time (Code-to-Production): 23 days, 16h/day (368 hours). Total development time (Code + Project Planning): 41 days (400 hours) (metrics for 1.3.0)

Total project usage of tokens, converted to USD, pre-subsidies: 6.756,70 USD (metrics for 1.3.0).
