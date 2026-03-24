# Malvertising PCAP Analysis — Fake Google Authenticator Delivery

## Overview
This is the Analysis of a malvertising infection where a user downloaded malware from a fake Google Authenticator site. This project documents the full investigation workflow: identifying the victim host, tracing the malware delivery chain, and uncovering C2 communication — written in the format of a SOC incident report.

**Exercise source:** [malware-traffic-analysis.net](https://www.malware-traffic-analysis.net/2025/01/22/index.html)  
**Threat intel reference:** [Unit 42 — Palo Alto Networks](https://github.com/PaloAltoNetworks/Unit42-timely-threat-intel/blob/main/2025-01-22-IOCs-for-malware-from-fake-Microsoft-Teams-site.txt)  
> This is a training exercise. All pcap data is from a controlled lab environment.

---
## Tools Used
- Wireshark
- Display filters: `http.request`, `dns`, `tcp.flags.syn == 1 && tcp.flags.ack == 0`
- Statistics > Protocol Hierarchy
- Statistics > Conversations
- Export Objects (HTTP)


---
## Environment
| Detail | Value |
|---|---|
| LAN Segment | 10.1.17.0/24 |
| Domain | bluemoontuesday.com |
| Domain Controller | 10.1.17.2 — WIN-GSH54QLW48D |
| Gateway | 10.1.17.1 |

---

## Scenario
A SOC analyst receives a report that a coworker downloaded a suspicious file after 
searching for Google Authenticator. A pcap of the associated traffic is retrieved for 
analysis. The objective is to identify the infected host, trace the infection vector, 
and document C2 activity for an incident report.

---

## Methodology
1. Loaded pcap into Wireshark and reviewed Protocol Hierarchy for traffic breakdown
2. Used DHCP and NetBIOS traffic to identify the infected host
3. Filtered DNS queries to trace the malware delivery domain
4. Reviewed HTTP objects to confirm malware download
5. Used Statistics > Conversations to identify repeated external connections indicative of C2 beaconing
6. Cross-referenced findings with Unit 42 threat intel IOC list

---

## Findings

### Victim Details
| Detail | Value |
|---|---|
| IP Address | 10.1.17.215 |
| MAC Address | 00:d0:b7:26:4a:74 |
| Hostname | DESKTOP-L8C5GSJ |
| Windows Username | shutchenson |

