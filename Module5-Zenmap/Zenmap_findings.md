# Module 5: Network Scanning with Zenmap

## Objective
Perform active network discovery on the local LAN subnet to identify live hosts, their IP addresses, and their MAC addresses, and generate a visual network topology.

## Methodology
1. Used Windows Command Prompt (`ipconfig`) to identify the local IPv4 address and Subnet Mask.
2. Calculated the local LAN subnet in CIDR notation (e.g., `192.168.x.0/24`).
3. Opened Zenmap (Nmap GUI) on Windows, entered the local subnet, and selected the **Ping Scan** profile to safely discover live hosts without aggressive port probing.
4. Used `getmac` / `ipconfig /all` to correlate the local machine's MAC address with the scan results.
5. Navigated to the **Topology** tab, enabled the legend, and exported the visual map as a PDF.

## Commands Used
```cmd
:: Identify local IP and Subnet
ipconfig

:: Identify local MAC address
getmac
:: OR
ipconfig /all
```

# Zenmap Target Input
```
192.168.x.0/24  # (Replace with your actual subnet)
# Profile: Ping Scan
```

### 📊 Scan Results Summary

#### Task 4: How many hosts are live in your subnet?
**Answer:** 1 host is live (including the local testing machine).

#### Task 5: What are the IP addresses of the live hosts?
| No. | Live Host IP Address |
| :--- | :--- |
| 1 | `192.168.204.1` |

#### Task 6: What are the MAC addresses of the live hosts?
| No. | MAC Address | Device/Notes |
| :--- | :--- | :--- |
| 1 | `78-BE-81-05-88-92` | Local Machine (Verified via `getmac`) |

> *Note: Full raw outputs are available in the `outputs/` directory of this module.*

---

### 🎯 Attacker Perspective (Why this matters)
While footprinting (Phases 1-4) is passive, network scanning is the first step of **active reconnaissance**. 

* **Discovering live hosts** allows an attacker to map the internal attack surface.
* **Identifying MAC addresses** can reveal device manufacturers (via OUI lookup), helping an attacker identify IoT devices, printers, or specific OS types to target.
* **Regular internal scanning** by defenders is critical to detect rogue devices, unauthorized access points, or compromised machines communicating on the network.
