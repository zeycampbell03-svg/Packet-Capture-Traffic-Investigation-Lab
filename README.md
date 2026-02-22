# Packet Capture & Traffic Investigation Lab

## Objective
Capture and analyze attacker-style reconnaissance traffic in a controlled virtual environment. Use Wireshark to identify SYN scan behavior and validate exposed services discovered during Nmap enumeration.

---

## Lab Environment
- Attacker Machine: Ubuntu Linux (VirtualBox)
- Target Machine: Windows 10 (VirtualBox)
- Tools Used: Nmap, Wireshark
- Network Configuration: VirtualBox internal network

---

## Reconnaissance Command
```bash
sudo nmap -sS -sV -T4 <target-ip>
```

---

## Findings (Open Ports)
- 80/tcp open  http (Microsoft IIS 10.0)
- 139/tcp open netbios-ssn
- 445/tcp open microsoft-ds

---

## Packet-Level Analysis (Wireshark)

### SYN Scan Evidence
Display filter used:
```text
tcp.flags.syn == 1 && tcp.flags.ack == 0
```
Observed high-volume SYN packets from the attacker host to multiple destination ports in a short time window, consistent with reconnaissance scanning.

### HTTP Traffic (Port 80)
Display filter used:
```text
tcp.port == 80
```
Confirmed full TCP handshakes and HTTP traffic consistent with an accessible web service.

### SMB Negotiation (Port 445)
Display filter used:
```text
tcp.port == 445
```
Observed SMB/NBSS negotiation traffic indicating the SMB service was reachable and responding to enumeration attempts.

---

## Skills Demonstrated
- Packet capture and analysis using Wireshark
- Identifying SYN scan behavior and reconnaissance indicators
- TCP handshake analysis (SYN → SYN/ACK → ACK)
- Service exposure validation (HTTP/SMB)
- Basic SOC-style network investigation workflow

---

## Files
- **Lab_Report.pdf** – Full write-up and findings
- **capture.pcapng** – Wireshark capture file
- **screenshots/** – Key evidence screenshots (filters + packet views)

---

## Key Takeaway
This lab demonstrates how reconnaissance activity appears at the packet level and how exposed services (HTTP/SMB) increase attack surface and lateral movement risk in enterprise environments.
