# Network Traffic Analysis with Wireshark: Identification of TCP and UDP Scanning Activity

## Objective
Analyze a packet capture (PCAP) to identify signs of TCP and UDP scanning behavior using Wireshark filters and traffic inspection techniques.

## Environment
- Tool: Wireshark  
- Source: TryHackMe Traffic Analysis Lab  
- File analyzed: exercise.pcapng  

## Methodology

### Initial Triage
Used Wireshark statistics and filters to obtain a high-level view of network activity and identify suspicious patterns.

### TCP SYN Scan Detection
Applied filters such as:

tcp.flags.syn == 1 and tcp.flags.ack == 0

Observed multiple SYN packets without full handshake completion, consistent with half-open scanning behavior.

### TCP Connect Scan Behavior
Identified full three-way handshakes in some connections, indicating complete TCP connect attempts.

### UDP Scan Analysis
Inspected UDP traffic and correlated with ICMP responses:

icmp.type == 3 and icmp.code == 3

This pattern suggested closed UDP ports and active probing activity.

## Key Findings
- Evidence of SYN-based scanning activity  
- Presence of full TCP connections to selected ports  
- UDP probing inferred through ICMP Port Unreachable responses  
- Traffic patterns consistent with reconnaissance behavior  

## Defensive Insights

From a Blue Team perspective, the observed traffic patterns are consistent with early-stage network reconnaissance. The presence of SYN packets across multiple destination ports, combined with ICMP Port Unreachable responses, indicates systematic probing activity.

Based on this analysis, a SOC analyst could monitor for indicators such as:

- High volumes of SYN packets targeting multiple ports from a single source.
- Repeated ICMP Type 3 Code 3 (Port Unreachable) responses.
- Short-lived or incomplete TCP connection attempts across many services.

These indicators may help identify potential scanning behavior during the reconnaissance phase of an attack. 

## Conclusion
The traffic analysis revealed clear indicators of potential network reconnaissance using both TCP and UDP techniques. Combining packet-level inspection with statistical analysis improves early detection of scanning behavior in SOC environments.

