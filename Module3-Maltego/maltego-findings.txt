# Module 3: Footprinting with Maltego

## Objective
Perform visual link analysis and OSINT gathering to harvest publicly associated email addresses for the target domain `networkwalks.com`.

## Methodology
1. Opened Maltego Community Edition (CE).
2. Dragged a **Domain** entity onto the graph and set the value to `networkwalks.com`.
3. Right-clicked the entity and executed email-related transforms (e.g., *To Email Addresses [from Domain]*, *Find Email Addresses [Search Engine]*).
4. Mapped the resulting connections and documented the harvested emails.

## Harvested Email Addresses
Below are the email addresses discovered during the passive reconnaissance phase:

| No. | Harvested Email Address | Source/Transform Used |
|-----|-------------------------|-----------------------|
| 1 | info@networkwalks.com | Domain to Email / WHOIS |
| 2 | support@networkwalks.com | Domain to Email / Search |
| 3 | [Add any other emails you found] | [Transform Used] |
| 4 | [Add any other emails you found] | [Transform Used] |
| 5 | [Add any other emails you found] | [Transform Used] |

*(Note: If Maltego CE limits the number of results, document whatever results were returned by the free tier).*

## Attacker Perspective (Why this matters)
Harvested email addresses are the primary fuel for **Spear-Phishing** and **Password Spraying** attacks. By knowing the exact email format (e.g., `firstname.lastname@networkwalks.com`), an attacker can guess other employee emails and launch targeted social engineering campaigns.