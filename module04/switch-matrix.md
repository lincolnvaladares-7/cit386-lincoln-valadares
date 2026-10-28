# CIT 386 — Module 4: Hyper-V Switch Reachability Matrix

**Student:** Lincoln Guimaraes Valadares  
**Evidence status:** Laboratory results and timing measurements still required. **Do not submit predicted outcomes as observations.**

## Tested reachability

Fill each cell with **Pass / Fail / Not tested**, using actual tests. For each target, record the command or method used (e.g., ping, HTTP, RDP), because firewall policy can affect the outcome.

| Hyper-V switch configuration | Guest → Host management OS | Guest → Other VM on same switch | Guest → Physical LAN device | Guest → Internet | Host management OS → LAN/Internet |
|---|---|---|---|---|---|
| External — share management OS adapter ON | Not tested | Not tested | Not tested | Not tested | Not tested |
| External — share management OS adapter OFF | Not tested | Not tested | Not tested | Not tested | Not tested |
| Internal | Not tested | Not tested | Not tested | Not tested | Not tested |
| Private | Not tested | Not tested | Not tested | Not tested | Not tested |

**Changed row when management OS sharing was toggled:** External switch — share adapter ON versus OFF.  
**Observed difference:** [Enter what changed in your lab; do not infer from documentation.]  
**Unexpected result (or pre-lab misconception):** [Describe a measured surprise, or what you previously expected incorrectly and why.]

## VirtualBox mapping

| Hyper-V switch | Closest VirtualBox networking mode | Qualification |
|---|---|---|
| External | Bridged Adapter | Both connect the guest to the physical network; Hyper-V management-OS adapter sharing adds a host-side distinction. |
| Internal | Host-only Adapter | Both support host-to-guest and guest-to-guest communication without direct external networking by default. |
| Private | Internal Network | Both isolate VM traffic from the host management OS and physical network by default. |

**Pairing that does not line up neatly:** Hyper-V External ↔ VirtualBox Bridged Adapter, particularly when management-OS adapter sharing is disabled; VirtualBox Bridged mode does not offer the same Hyper-V host-vNIC sharing toggle. VirtualBox NAT also has no direct counterpart among these three Hyper-V switch types without additional routing/NAT configuration.

## VirtualBox timing comparison

| Configuration | Measured time (seconds) | Test operation |
|---|---|---|
| Hyper-V platform OFF | Not measured | [Enter boot/start operation] |
| Hyper-V platform ON | Not measured | [Use same operation] |

**Two-sentence explanation:** With the Hyper-V platform off, VirtualBox may use its own hardware-virtualization path directly. With Hyper-V enabled, VirtualBox may run through the Windows Hypervisor Platform/Hyper-V hypervisor layer, changing its virtualization backend and potentially its performance.

## Publishing and validation log

- Public resume URL: **[Add actual deployed URL]**
- Assigned shared-storage directory: **[Add assigned directory]**
- Uploaded `index.html` and `resume.pdf`: **[Confirm]**
- Static website hosting/default index document configured: **[Confirm]**
- PDF `Content-Type: application/pdf` checked: **[Confirm; record any fix]**
- Tested in private browser: **[Confirm]**
- Tested on phone: **[Confirm]**
- Tested on a second, signed-out computer: **[Confirm]**
