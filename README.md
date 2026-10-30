
# Network Walks - Cybersecurity Internship 2026
## Task WK1-PM1: VirtualBox & Kali Linux Lab Setup

### Overview
This repository documents the foundational lab environment configuration for Task WK1-PM1 under the Network Walks Cybersecurity Internship 2026[cite: 3, 4]. The objective was to configure an isolated testing subnet, configure a Kali Linux attacking machine with a static IP and full internet connectivity, configure host integration features, and capture a baseline snapshot[cite: 4, 6].

---

### Network Architecture & Specifications
* **Hypervisor:** Oracle VM VirtualBox[cite: 4, 6]
* **Network Mode:** NATNetwork (`NatNetwork`)[cite: 4, 7]
* **Subnet:** `10.0.0.0/24`[cite: 4, 7]
* **Default Gateway:** `10.0.0.1`[cite: 9]
* **Attacker Machine:** Kali Linux[cite: 4, 6]
* **Static IP Assignment:** `10.0.0.2/24`
* **DNS Resolution:** `8.8.8.8` / `10.0.0.1`[cite: 9]
* **Host Integration:** Bidirectional Shared Clipboard, Bidirectional Drag & Drop[cite: 4]
* **Shared Storage:** Host `/Downloads` folder mapped with auto-mount enabled[cite: 4, 11]

---

### Lab Configuration & Verification Proof

#### 1. NATNetwork Configuration
Configured a custom NATNetwork in VirtualBox with subnet `10.0.0.0/24` and DHCP enabled[cite: 4, 7].

![NATNetwork Configuration](01_virtualbox_natnetwork_10.0.0.0_subnet.png)

---

#### 2. Host Shared Folder (`/Downloads`)
Mounted the host machine's Downloads folder with auto-mount and full read/write permissions for seamless file exchange between the host and Kali Linux[cite: 4, 11].

![Shared Folder Configuration](02_virtualbox_shared_folder_downloads.png)

---

#### 3. Bidirectional Clipboard & Drag and Drop
Configured both Shared Clipboard and Drag'n'Drop to Bidirectional mode in the VM settings[cite: 4].

![Clipboard and Drag Drop](03_kali_vm_bidirectional_drag_drop_clipboard.png)

---

#### 4. Static IP & Gateway Configuration
Assigned `10.0.0.2/24` manually to the network interface in Kali Linux and verified the default route pointing to gateway `10.0.0.1`[cite: 4, 9].

`bash
ip a
ip route
5. Network Connectivity & Internet Access
Tested end-to-end packet transmission to the default gateway, public IP, and DNS domain resolution with 0% packet loss[cite: 4, 9].

Plaintext
ping -c 4 10.0.0.1
ping -c 4 8.8.8.8
ping -c 4 google.com
6. Baseline Clean Snapshot
Created a clean baseline snapshot in VirtualBox to preserve the working state before running future security tests[cite: 6].

Technical Troubleshooting Note
On modern VirtualBox and Kali Linux releases, duplicate address detection can prevent the static interface from binding correctly[cite: 10]. This was resolved via NetworkManager CLI[cite: 10]:

Plaintext
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
