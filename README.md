# Purple Team Lab: Attack & Detection Engineering
Author: Suriyah Saravanan<br>Role: Security Researcher/Purple Team Analyst
---

## Lab Overview & Architecture

This project demonstrates the implementation of a full-stack security monitoring environment. The objective was to execute a Point-to-Point exploit and engineer custom detection rules within a SIEM to identify malicious activity in real-time.

    Blue Team (SIEM): Wazuh Manager & Indexer (v4.14) running on Ubuntu Server.

    Red Team (Attacker): Kali Linux utilizing the Metasploit Framework.

    Target (Victim): Metasploitable 2 (Linux-based vulnerable VM).

    Hypervisor: Oracle VirtualBox.
---
## Red Team Phase: The Exploit

Objective: Gain unauthorized root access to the target via a known backdoor.

    Vulnerability: vsftpd 2.3.4 Backdoor Command Execution.

    Payload: cmd/unix/interact.

    Execution: I utilized Metasploit to target the victim at 10.0.2.3. By exploiting a backdoor in the FTP service, I successfully spawned a root shell, allowing for full system compromise.
---
## Blue Team Phase: Detection & SIEM Analysis

Objective: Monitor the attack lifecycle and verify log integrity within the Wazuh SIEM.

    Log Ingestion: Configured Wazuh agents to monitor the victim's auth logs and system activity.

    Detection Strategy: I executed a custom "Pipeline Test" by injecting a uniquely tagged string (SURIYAH PIPELINE TEST) into the victim's logs using the logger command.

    SIEM Visualization: Verified that the Wazuh manager successfully parsed the log, categorized the event, and displayed the activity in the Discover dashboard.

    Incident Response: Identified the exploit attempt by monitoring for vsftpd service crashes and unexpected root-level shell spawns.
---
## The Purple Team Outcome

The value of this lab was the verification of the Security Pipeline.

    Attack: The Red Team established a point-to-point connection and achieved root.

    Telemetry: The Blue Team verified that the SIEM was not "blind" to the attack.

    Optimization: This lab provided the baseline for tuning Wazuh alerts to specifically flag vsftpd backdoor patterns and unauthorized sudo executions.
---
## Technical Evidence

(In GitHub repo, place images in an /assets folder and link here)

    Red Team Success: Achieving root shell via Metasploit.

    Blue Team Monitoring: Wazuh Discover dashboard showing vsftpd activity and my custom pipeline watermark.
---
## Tech Stack

    SIEM: Wazuh (Elasticsearch/Filebeat/Kibana stack)

    Exploitation: Kali Linux / Metasploit

    Virtualization: Oracle VirtualBox / OVA management

    Networking: Host-only Adapters / Internal DHCP
