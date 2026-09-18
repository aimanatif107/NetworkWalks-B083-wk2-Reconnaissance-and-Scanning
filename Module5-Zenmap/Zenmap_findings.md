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