# Module 4: Footprinting with theHarvester

## Objective
Automate passive OSINT gathering to harvest email addresses, subdomains, and hosts related to the target domain `microsoft.com` using public data sources.

## Methodology
Executed `theHarvester` in Kali Linux against `microsoft.com` using two different configurations:
1. **Task 1:** Queried the **Baidu** search engine with a high result limit (1000) to find indexed data.
2. **Task 2:** Queried **all** supported public sources (PGP servers, Shodan, search engines, etc.) with a lower limit (50) to prevent API rate-limiting while maximizing source diversity.

## Commands Used
```bash
# Task 1
theHarvester -d microsoft.com -l 1000 -b baidu

# Task 2
theHarvester -d microsoft.com -l 50 -b all