List of versions and their changes at C-Servers EagleKey.

v3.3.1-v3.3.8
- Improvements and bug fixing - August 31st to September 6th, 2026
- CHV treatment has been improved, including a race condition of 1 second between operations that could cause a reinstall to fail
- Upgrades the EagleKey Control to better reflect new offerings, with full IPv4s
- A watcher is now available for tunnels and BGP propagation that continuously ensures these are up, but also accounts if these fail in a loop and reports.
- Tighter integration between EagleKey and BIRD: a /32 or higher on IPv4 and a /64 or higher on IPv6 can be automatically provisioned from iBGP and ensure connectivity to the ASN. Opens ports to possible future automated BGP downstream announcements provided to users (at present these are manually held).
- NAT improvements: the 1st port is always published prior to the 1st VM on an hypervisor and SNAT now covers for specific tunneling when the IP used on a NAT service is part of a public tunneled/BGP-communicated range
- Significant improvements taken at EK on the 1st deployment of a NAT-based, /32 IPv4 and /48 IPv6 system at C-Servers with all IPs using AS214566, Zeta.12 Ashburn, which also uses tunnelled communication between two Ashburn endpoints. Internal configuration at the Ashburn dedicated server ensures fast performance and effectiveness on the first of new configurations and global networking independence. Usually server panels do not account for any tunelling - that happens here, starting from v3.3.7.
- Triple communication between the WebStore, EagleKey and external API junctions for product management and communication via automatic CLI scripting, which will allow for automatic product updates and stock updates at different sales platforms - major advance.
- Fixes a pre-reinstall MTU provisioning bug affecting a small portion of users.

v3.3.0 
- Improvements - August 28th to 30th, 2026
- Security improvements and code cleanup ahead of dedicated IPv4 launch
- New "Security" area, encompassing FloodGuard, CPU/disk/network abuse and similar correlated areas
- New "Safety Center" area, encompassing 22 public lists for IP blacklisting/activity covering all IPv6 and IPv4 addresses, plus a IDS/IPS now embedded into the system (Stratospheric Linux IPS - SLIPS, a ML fine-tuned project existing since 2012 and based in Prague), with direct reporting, classification and log retention, by default on IDS mode. This will help with any immediate adjustments required for any IP usage to ensure cleanliness and ensuring available information is always up to date.
- Automatic e-mail notifications to all system administrators as soon as any IP of the covered listings is blacklisted
- New RBAC covered option for staff/customer service agents including these listings.
- New customized text screen after each deployment or when Internet momentarily failures occur, "The EagleKey Server Portal will return in a few moments...". This should improve the user experience in comparison with Blazor Server's default.
- NAT ports are now specifically labelled by default and mapped per-VM for convenience.
- Correlation and overlapping errors on NAT ports permanently fixed and reconciled (2 VM's with same ports - operation unaffected).
- Agent now does automatic VM reconcilliation between any possible classification drifts of CHV or QEMU on the DB with the corresponding valid signals, as humanly mandated; and code is now improved in tandem to further restrict and avoid these. These don't affect user operation, but DB reliability is essential and further ensured with these changes, improving general system operation.
- Multiple new E2E tests accross features to ensure more reliability.

v3.2.0.1
- Fast-track improvements - August 27th, 2026
- Significantly improves RAM consumption of VictoriaMetrics and of the .NET / Blazor Server system. 
- Improves RAM consumption of the agent, reduces unnecessary static calls.
- Global reduction of 800MB on RAM consumption - the panel now starts with 1.2GB RAM consumption only. Recommended RAM ballpark now at 3GB + 3GB zRam Swap; disk recommendation now minimum SSD or higher.
- Improvements on IPv6 handling

v3.2.0
- Minor version launch, including a bug fixing and improvements roundup - August 27th, 2026 
- Fixes a very specific flapping bug where a suspended VM could get an error from virsh and leave a VM in an inconsistent state between the Postgre control DB, the server and the system, leaving the VM accessible over SSH but inaccessible on the platform. 
- Reorganizes the few post-VF migrated still-pending network blocks by hypervisor, leaving them displayed on the Admin area as summarized by default instead of expanded per-hypervisor
- Introduces a new menu, "Port forwarding", that conveniently lists in one place all active port forwardings on the NAT service
- Introduces a new menu, "Self Healing", that is directed at sorting out the most frequent errors on this panel and immediately gaining visibility on any future errors that occur. It diagnoses and solves, automatically or manually, any possible errors on 5 fronts (for now): networking, VM reconcile, Backups, Storage and Datastores, and Updates.
- Error messages and general comments on the code are now entirely written in English; previously one of the builders wrote them in Portuguese, which ultimately caused some of the possible comments or error messages to arrive in Portuguese. This is now fixed, with special attention for front-facing user error messages.
- General efficiency improvements.

v3.1.2-v3.1.5
- Bug fixing and improvements roundup - August 14th to August 24th, 2026
- Fixes 2 permission bugs on CHV
- Improves handling of dedicated IPv4 IPs and interfaces
- One-to-many approach : one user reporting an issue needs to be confirmed if the issue is global;
- Fixes some IPv6 NDP provisioning issues and information reconcilliation issues
- Introduces for the first time DeepSeek v4 Pro-0813 as a coding agent for deliberately non-Western security counteranalysis, punctual adjustments and general coding improvements, including on topics top-tier Western models may struggle.

v3.1.1-v3.1.2
- Bug fixing and improvements roundup - August 12th, 2026
- Fixes a bug with uppercase letters on e-mails saying that an account was suspended due to a null pointer. 49 users affected but now fixed.
- Improves per-VM isolation accross the fleet
- virtio-net and virtio-blk now with multiqueue implemented, with value equal to the number of vCPUs, up to 16
- Simplification and cleanup of the Admin Area Dashboard presentation and menus
- Simplification and cleanup of the Client Area presentation to avoid duplicates
- Fixes a long-standing bug due to PTY buffering on the Admin Area console (CHV-only and intermittent).

v3.1.0
- Minor Version Launch - August 11th, 2026
- Strongly improves and tests direct migrations for full reliability, correcting the in-flight GUI system and ensuring all launched migrations occur successfully.
- Fixes a nftables syntax bug reported on the Support area
- Fixes a minor one-off reinstall lock bug reported on the Support area
- Removes the "Suspend" button from the Lite version of EagleKey for parity with the primary version
- Performance, reliability and responsitivity improvements on the called functions and the general interface at the Admin and Client areas.

v3.0.1-v3.0.2
- Bug fixing and improvements roundup - August 8th-10th, 2026
- Fixes an inconsistent lock that occurred to some automated VM backups over restic
- Adds to the EagleKey module at the billing system automatic provisioning tested E2E of add-ons for CPU, RAM, HDD, traffic and IPs 
- Fixes an inconsistent state that rarely occurred on the billing system in direct communication with EagleKey - the VM would still be cancelled or suspended, but the correct feedback would not arrive in time. This doesn't ever happen now.
- General significant performance improvements with deserialization, splitting and lower statistical request polling to VictoriaMetrics
- Changes the Disk Abuse mechanism from calculation ratios over a regular speed, to a anomaly-based detection that partially borrows from CPU Abuse mechanisms, significantly improving reliability at detection and suspensions by direct I/O measurement
- Fluidity and design improvements on the interface at the Admin and Client areas
- Improves VNC security
- Fixes a HTTP/3 bug where VNC and sometimes Console would not work on some privacy-focused browsers, or would work inconsistently
- Fixes some too literal translations (i18n) in Portuguese, French and German
- Fixes a bug where ISO storage rules were not yet being applied due to a cross-rule.

<b> v3.0 </b>
- Major Version Launch - August 6th, 2026
- More than 140 minor remaining bugs fixed and more than 60 adjustments/improvements done
- Improvements on Backup execution and display
- New professionally designed logo
- General performance improvements

v2.2.17-v2.2.26
- Bug fixing roundup (July 21st to August 1st, 2026)
- Fixes some backup issues related to manual backups and logins to the backup node that prevented adequate backup execution
- Fixes a bug on EL10 installs where QEMU and libvirt agents weren't updated to reflect EL10 differences, and introduces bridging naming to the several internal tools at Libvirt for parity with Debian
- Fixes a resizing issue on CHV servers at the Admin Area, including package changes
- Fixes a bug at Status where removing more than 1 warning would crash the panel
- Introduces some underlying differences regarding full IPv4 servicing subnets and not only NAT ones
- Introduces more verbose errors regarding migrations on CHV and QEMU for adjustment
- Fixes 3 bugs related to internal DR (Disaster Recovery) upon reprovisioning of a new server when occurring on a different system (EL10 vs Debian-based)
- Fixes definitively the inconsistency of states between QEMU and CHV migrations, that still occurred with 1% of the VM installs, with a watchdog that applies predefined and validated rules to always show the correct variant according to the OS and the version (QEMU or CHV) at any given moment
- General E2E tests for continuous validation and other minor adjustments

v2.1.6-v2.2.17
- Feature improvement, minor version bump and several minor bug fixing rounds (July 13th to 20th, 2026)
- Reimplements the Admin Area fix for serial console access (post-restart regression now fixed)
- Fixes a login issue that ocasionally happenned where the Portal would still be up but logins weren't available
- Improvements to RAM consumption on the control system (logging behaviour changed)
- Introduces --pvpanic to generate restarts following kernel panic on QEMU and CHV; later temporarily removed on CHV due to technical issues and adjusted on QEMU to change the kernel panic device detector from a ISA to a PCI-E device
- Fixes CHV permission issues seen on some reinstalls, post-implementation of the kernel panic device (regression fixed)
- Improves e-mail warnings regarding server networking abuse by including distinction between outgoing and incoming (dispensing further verification), showing hits per 45 seconds instead of global for every 12 hours (digest still every 12h)
- Improves serialization of provisioning, suspension and deletion and multi-threading on those actions, to make them more reliable
- Fixes an introduced bug where a resource abuse suspended customer could still contour that suspension by merely clicking on Start or Restart, now power actions are locked at the panel level
- Introduces FloodGuard: a directly made rate limit for port scanning, dynamic on speed, activated/deactivated on a per-plan, per-VM and per-server basis, automatically imposed and automatically raised, always informed via e-mail to the sysadmins, which doesn't substitute terminations for port scanning but rather very much improves responsivity for these issues and cuts the abuser more proactively,
- Introduces prohibiting IP spoofing on the system (a feature that previously existed on SolusVM 2 and essential on NAT environments).
- Introduces an automatic system guard that detects failures of the Portal and then restarts it in full automatically, ending downtimes for that reason and improving stability
- Improves suspension reliability

v2.1.0-v2.1.6
- Feature improvement, minor version bump, and minor bug fixing round (July 12th, 2026)
- Fixes some minor and specific translations in non-English or non-Portuguese languages on the Admin Area
- Fixes a RAM cosmetic presentation bug that affected sub-1GB RAM packages, and non-rounded packages, on the Admin Area and the Client Area
- Fixes a bug on the Admin Area with Console presentation cutting mid-way on CHV, and the fallback to virsh on some edge cases at the Client Area (not noticed by the customer)
- Fixes IPv4 NAT cosmetic counting on internal blocks
- Fixes a minor bug on the Mailout where a VM that was already suspended prior to mail-sending did not count as a valid recipient, it now counts
- Implements CLI DR (Disaster Recovery)
- Implements improvements to the CPU Abuse and Network Abuse mechanisms, improving classification
- Implements improvements to the Backup Manager

v2.0.30-v2.0.37
- Minor remaining bugs' flash round and improvements round (July 6th, 2026)
- Fixes a punctual login issue caused due to a minor call on 1 of the changes inserted on the previous round
- Fixes a clipboard inconsistent issue that happenned on Firefox and Safari; on Chrome this issue only happenned if the window wasn't focused
- Fixes a suspension issue at the WiseCP module where suspensions were not being launched with an error code or with a JSON message
- Fixes an upgrade issue where upgraded packages were not reflecting the specifications automatically on a VPS system
- Fixes an incorrect behaviour where some CHV VM's were cosmetically having the network named on GUI as "default" instead of the correct interface (at Admin Area)
- Introduces full CHV migration between dedicated servers
- Introduces a abusecore section that handles CPU, Network and Disk abuses in one place
- Introduces multithreading to iperf3 for 10/25/40 Gbps servers
- Introduces a second long-poll tiered CPU Abuse reading, where inconsistent usage seen as over the limit, on a longer analyzed period of time, also triggers escalations, which improves accuracy.
- Introduces a circuit conversion on IDbContextFactory to further improve efficiency
- Introduces sync-over-async to improve reliability
- Introduces specialized configurations for legacy systems for Windows and Linux (pre-2004), including 60fps Game Mode, sound-on-browser, USB/SCSI peripheral utilization, on-sync multiplayer controls, with ultra low latency, for a specialized product.

v2.0.28-v2.0.29
- Minor remaining bugs' flash round (July 3rd and 4th, 2026)
- Fixes a minor provisioning location error where only 3 packages were registering as "None" instead of the correct location.
- Fixes two observed memory leaks regarding metrics management on the control-VictoriaMetrics communication. Ensures that no further memory leaks exist. The panel is now fully RAM-stable. 
- Fixes rDNS, allowing Manual, Bunny.net or PowerDNS, and migrates rDNS records previously registered at VF. No downtime was incurred. rDNS is now fully operational.
- Fixes all HAProxy-detected issues and migrates domains from the previous table to a new table. No downtime was incurred on 99.6% of the existing websites. HAProxy is now fully operational. 
- Fixes a CPU Abuse automation error where recurrence of abuses wasn't displaying correctly on GUI and did not increase suspension periods as recurrences ocurred.
- Fixes a CPU Abuse display bug where history of suspensions was not displaying correctly and was at another section
- Introduces CPU Abuse per-plan percentage granularity with optional overrides of the global CPU setting for CPU Abuse, re-tested to ensure it works accordingly. Previously only a Global value existed.
- Fixes a Observability display bug where, under Benchmarks, Disk tests history were appearing at Network.
- Fixes a minor bug seen on 1 user regarding two IPv6 IP addresses appearing - the condition was not reproducible, this was after migration, but it's sorted out.
- Introduces per-plan fallback location mapping that covers the "None" settings on the WiseCP module for location/servers, preventing allocation to different servers than the ones intended, through direct allocation
- Fixes a rare bug seen where 5 VMs got "Awaiting Setup" status but were actually working and accessible, which only occurred when deployments / panel refreshes coincided with reinstalls. A guardrail now exists that looks for servers on these status and conveniently completes any pending reinstalls or panel reconcilliations.
- Fixes a condition where migrating from a SSH Linux/BSD system to a Windows system didn't change the ports and the port forwarding from SSH to RDP, and another one on 1st install that deployed Windows VMs with SSH instead of RDP. 
- Fixes a minor bug where the Benchmark section (Admin area) shows only 1 iperf3 server to test manually instead of the full available listing, and where iperf3 execution to external servers (for Network Abuse evaluation) fails with a signal or an empty string.

v2.0.21-v2.0.27
- Bug correction flash round versioning publicly available (July 2nd, 2026)
- Fixes IPv6 display on the panel and shows it adequately in accordance with the existing IPv6 IPs
- Fixes IPv6 deployment: previous VF-migrated customers have non-DHCP provided fixed IPv6 IPs, these are respected and maintained with connectivity; upon reinstall, fixed IPv6 IPs are now provided by default with RA, SLAAC and EUI-64 automatically, in accordance with the most recent sector practices, and displayed correctly on the platform. EagleKey is now the most IPv6-compliant panel on the market.
- Fixes a minor display synchronization IP bug on the database (affecting only 4 VMs) following the many networking changes done and resets parity permanently from now on.
- Fixes something that is not EagleKey's responsibility: Ubuntu 26.04 LTS, 24.04 LTS and 22.04 LTS default to allowing only public keys and not passwords. We have corrected that behaviour on the template, and now allows password + public keys. Debian 12/13 and other systems were also checked preventively.
- Improves ISO handling on QEMU/KVM systems.
- Fixes Windows Server IPv6 deployments that were briefly providing a random address before the final one was provided.
- Fixes IPv4 NAT registration fallbacks on Windows Server over IPv4 to always behave as intended.

v2.0.1-v2.0.20
- Bug correction flash round versioning publicly available (July 1st, 2026)
- Fixes a IPv4 NAT provisioning error on QEMU-to-CHV where IPv4 NAT IP was not being passed on in some isolated use-cases
- Fixes read-ahead for an issue between PrimaryIpv4 and ip_addresses incorrectly failing to provision the remaining isolated use-cases
- Fixes GC mode for .NET engine from Server to Workstation (GUI Admin/Staff/Client Area): was becoming less stable every 12-16 hours due to thrashing
- Fixes 3 minor race conditions that caused one-off errors due to concurrent activities (on reinstall and NAT management)
- Fixes inconsistency on reinstall GUI showdown and network provisioning by including one last step that awaits for cloud-init and the VM to post OK
- Fixes IPv6 Route Block to provide a /126 under natbr0 and not MacVTap only for hypervisors where IPv6 RB is used, on newer CHV and QEMU-to-CHV reinstalls through proxying+NDP at these hypervisors only, whenever there's only one /64 IPv6 available
- Fixes Flush NAT button not allowing NAT to be flushed on non-DHCP servers
- Fixes incorrect MTUs on the previous VirtFusion setup at some servers and defines default at 1500 with TCP MSS Clamp and PM; now also customizable
- Fixes a major bug where transient middle-of-the road states between QEMU and CHV left servers SSH-reachable, but did not provide VNC or Console access, due to libvirt leftovers. Now maps correctly Name or UUID and redirects to the next active domain (QEMU or CHV) » fix is QEMU-to-CHV and CHV-to-QEMU safe
- Fixes reinstall inconsistent failures on QEMU-to-CHV leaving the VM in an unusable state without domain at QEMU or CHV, now pre-validates status availability upon reinstall and executes rollback to the prior state on QEMU or CHV if necessary.
- Fixes permission errors blocking reinstall and creates an agent that continuously verifies, and if necessary rechanges, directory and file permissions, so that the issues don't happen again
- Fixes CPU Abuse operation not sending e-mails by marking these e-mails as transactional
- Fixes CPU Abuse operation not suspending VMs by incorrectly reading cgroups and libvirt states
- Fixes CPU Abuse operation sending e-mails with incorrect CPU load percentages above 100%, defaulted to 0-100%
- Fixes CPU Abuse operation for CHV setups, not only QEMU ones
- Fixes abuse level stepping on CPU Abuse, Network Abuse and Disk Abuse to correctly reflect reasonable defaults
- Fixes Traffic Shaping defaulting to KVM-only and not allowing CHV: now can operate on both
- Fixes fio/iperf3 benchmarks not posting to EagleKey and fio benchmarks not loading on ZFS systems
- Fixes incorrect servers for iperf3 benchmarks and creates a new function where the server can be specified
- Fixes an incorrect transient state post-migration where VMs were posted to .../eaglekey/vms instead of the correct VM dedicated pool, corrected and VMs migrated to the correct pool (5 new VMs affected)
- Introduces a 6th screen on deployment of new hypervisors allowing for auto datastore detection or manual
- Introduces Free Page Reporting as active on all hypervisors under KVM » significant improvements on RAM handling, CPU performance and I/O performance 
- Introduces KVM auto-deflate on QEMU and CHV domains active by default 
- Allows ksmtuned (if applicable) to use Smart Agent (introduced on Linux 6.7)
- Changes fallback zram lz4 (if applicable and used) to use vm.page-cluster=0 instead of =3 » significant improvements on RAM latency and IOPS by default
- Fixes a severe balooning issue caused by Cursor on June 14th writing where virsh setmem, if defined, was defined to actually preset all RAM at all VMs to the balooning amount and not to the present RAM minus the balooning amount, which would have caused all VMs to stall. Corrected to define balloning accordingly.
- Fixes balooning and observability areas where a JWT or hv_id error was posting to EK, now working correctly
- Introduces asynchronous provisioning and asynchronous suspension with Name or UUID read to account for QEMU and CHV VM's
- Introduces a Console button on the WiseCP EK module
- Fixes a relevant bug where VM product (billing) without any server ID or user ID would default to post the first VM on the list, of a third-party real customer, though unmanageable. Now returns N/A or the correct VM.
- Fixes minor remaining MASQUERADE rules from VirtFusion (0.1%) that were still using iptables and not nftables
- Introduces improvements to reinstall handling that significantly increase reliability for the end-customer
- Introduces Windows Server templates with windows-modern hardware profile for 2019, 2022 and 2025
- Fixes some inconsistent remaining code errors affecting a select few customers where their IP was not provisioned correctly due to cloudinit errors
- Massively cross-retested 8-10 continuous OS changes QEMU » QEMU, QEMU » CHV, CHV » CHV and CHV » QEMU pairings to ensure reliability and fixing bugs
- Fixes some packages automatically defaulting internally post-migration push to KVM-only instead of QEMU+KVM, and not allowing CHV OS installs, which caused some errors and some tickets; all are now cross-platform.

v2.0.0
- Second stable version publicly available (June 30th, 2026)
- (Fix) Billing system » Control Server corrected issues on provisioning (wrong network interface, suspensions not arriving)
- (Fix) Reinstall inconsistencies on QEMU-to-CHV (CHV-to-CHV and QEMU-to-QEMU was working correctly since 1.3.0)
- (Fix) Networking issues upon provisioning on some QEMU-to-CHV converted servers corrected (IPs provisioned blank due to cloud-init fault)

v1.3.0 
- First stable version publicly available (June 27th, 2026)

