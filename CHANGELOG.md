List of versions and their changes at C-Servers EagleKey.

v2.0.21-v2.0.22
- Bug correction flash round versioning publicly available (July 2nd, 2026)
- Fixes IPv6 display on the panel and shows it adequately in accordance with the existing IPv6 IPs
- Fixes IPv6 deployment: previous VF-migrated customers have non-DHCP provided fixed IPv6 IPs, these are respected and maintained with connectivity; upon reinstall, fixed IPv6 /64 and /126 IPs are now provided by default with RA, SLAAC, DHCPv6 and EUI-64 automatically, in accordance with the most recent sector practices, and displayed correctly on the platform. EagleKey is now the most IPv6-compliant panel on the market.
- Fixes a minor synchronization IP bug on the database (affecting only 4 VMs) following the many networking changes done and resets parity permanently from now on.

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
- Fixes a relevant bug where VMs without any server ID or user ID would post the first VM on the list, of a third-party real customer, though unmanageable. Now returns N/A or the correct VM
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

