# CyberSecOps-Lab-ELK-Stack-Mythic-C2-osTicket-

A hands-on cybersecurity project designed to simulate a real-world Security Operations Center (SOC) environment. This lab integrates various open-source tools to detect, investigate, and respond to simulated cyber threats, providing a comprehensive learning experience.

A full walkthrough of this project into detail can be found on Stephen's MYDFIR Youtube Channel [here](https://www.youtube.com/watch?v=GWX19cpv21w&list=PLG6KGSNK4PuBb0OjyDIdACZnb8AoNBeq6) 

## Cybersecurity Project Documentation

**Project Title:**

CyberSecOps Lab: Real-World Threat Detection, Incident Response, and Adversary Emulation.

**Introduction**

In this project, we developed a robust cybersecurity lab environment hosted on Vultr, meticulously designed to emulate real-world attack and defense scenarios. This environment integrates industry-standard tools such as the Elastic Stack for log aggregation and detection, osTicket for incident management, and Mythic for adversary emulation.

The project simulates the full threat lifecycle, from initial access through exfiltration, showcasing complex attack chains and enabling detailed analysis through custom-built dashboards. Our SOC workflow ties detection to response through automated alerting and ticketing, creating a realistic Security Operations Center environment. By replicating tactics, techniques, and procedures (TTPs) aligned with the MITRE ATT&CK framework, the lab provides a comprehensive platform for threat intelligence, continuous monitoring, and proactive defense strategies.

The environment also supports hands-on experimentation with advanced defensive capabilities, like Elastic Defend, which provides real-time endpoint monitoring and threat containment. This project serves as an invaluable learning tool, laying the groundwork for future research and development in cybersecurity defense, threat hunting, and SOC optimization.

## Logical Diagrams

![SOC-Mini-lab drawio](https://github.com/user-attachments/assets/dcc81b1b-5bf3-4288-91c7-87b0e039f1be)

Understanding the logical layout of the environment is essential for grasping how different components interact. The logical diagram illustrates the architecture, including virtual private cloud (VPC) networking, server roles, and the flow of data between systems.

* **SOC Analyst Laptop:** Connects to the Elastic and Kibana stack via a web GUI to monitor incoming logs and alerts.
* **Elastic & Kibana Server:** Manages log data ingestion, visualizes security events, and provides real-time analysis.
* **Fleet Server:** Orchestrates and manages endpoint agents, collecting logs and forwarding them to Elastic.
* **osTicket Server:** Handles alert tickets generated by security events, enabling incident tracking and management.
* **Mythic C2 Server:** Simulates an attacker’s command and control infrastructure, facilitating penetration testing and red team activities.
* **Windows & Ubuntu Servers:** Act as endpoints, mimicking production systems, with logging agents forwarding activity data for analysis.

The logical design is structured to reflect the communication pathways between systems, with private IP addressing and controlled access points. This architecture ensures realistic network behavior and supports complex threat detection scenarios.

![Cloud-Project-Devices](https://github.com/user-attachments/assets/a711b05b-79d6-4fc8-a4ab-7fc5f371cb1f)

## ELK Stack

The ELK Stack, composed of Elasticsearch, Logstash, and Kibana, is a powerful suite of tools used for log management, search, and data visualization. It is widely adopted in cybersecurity for centralizing and analyzing logs, making it easier to detect threats and investigate incidents.

* **Elasticsearch:** A distributed search and analytics engine that stores and indexes log data.
* **Logstash:** A data processing pipeline that collects, transforms, and ships logs to Elasticsearch.
* **Kibana:** A visualization tool that works with Elasticsearch to create dashboards, graphs, and charts for analyzing log data.

### Installation of ELK Stack

Rather than listing every installation command, below are some useful resources that provide detailed guidance on setting up the ELK Stack:

* What is ELK Stack? [Watch the video](https://www.youtube.com/watch?v=4AwBhXAW90Q)
* Elasticsearch Setup Guide: [Watch the video](https://www.youtube.com/watch?v=ypXARA5Uk4I)
* Kibana Setup Tutorial: [Watch the video](https://www.youtube.com/watch?v=tXwMoBbrkYw)

These resources will walk you through the installation, configuration, and initial setup, allowing you to build and configure your ELK environment step by step.

## Elastic Agents and Fleet Server

Elastic Agents and the Fleet server are essential components for collecting, managing, and forwarding logs from various endpoints to the ELK stack.

* **Elastic Agent:** A single, unified agent that collects logs, metrics, and security data from your servers and forwards it to Elasticsearch. It replaces older Beats agents (like Filebeat and Metricbeat) for a more streamlined, modern approach.
* **Fleet Server:** Acts as the central management system for Elastic Agents, allowing you to configure, monitor, and update agents at scale. It simplifies deploying and managing agents across multiple endpoints.

Elastic Agents can be installed on various systems (Windows, Linux, macOS) to collect and ship data like system logs, audit logs, network activity, and more, which can then be visualized and analyzed in Kibana.

### Setting up Elastic Agents and Fleet Server

For a step-by-step setup guide, check out this useful video resource:

* Elastic Agents & Fleet Server Setup: [Watch the video](https://www.youtube.com/watch?v=P2SFC6Kwae0)

This video will guide you through installing the Fleet server, enrolling agents, and verifying data ingestion into the ELK stack.

## Sysmon (System Monitor)

Sysmon (System Monitor) is a Windows system service and device driver that logs detailed information about system activity to the Windows Event Log. It is an essential tool for security monitoring, as it provides deep visibility into system events such as process creations, network connections, and changes to file creation timestamps.

Sysmon enhances endpoint visibility and works seamlessly with Elastic Agents to forward logs to Elasticsearch for analysis and correlation.

* **Process Monitoring:** Tracks process creations, including command-line arguments, to detect suspicious activity.
* **Network Monitoring:** Captures outbound network connections, showing the source, destination, and process that initiated the connection.
* **File Hashing:** Records cryptographic hashes of files, aiding in threat-hunting and malware analysis.

### Installing Sysmon and Integrating with Elastic Agent

Installing Sysmon involves downloading and configuring it with a ruleset that specifies which events to log. Once installed, the Elastic Agent can be configured to collect and forward Sysmon logs to Elasticsearch, where they can be visualized and analyzed in Kibana.

For a complete setup guide, check out this detailed video walkthrough:

* Sysmon Setup and Integration with Elastic Agent: [Watch the video](https://www.youtube.com/watch?v=nzZY9OSfkeg)

This video provides step-by-step instructions on installing Sysmon, configuring the rules, and setting up the Elastic Agent to ship logs to your ELK stack.

## RDP (Remote Desktop Protocol)

Remote Desktop Protocol (RDP) is a proprietary protocol developed by Microsoft that allows users to remotely connect to and control another computer over a network connection. It is commonly used for remote system administration and support but can become a significant attack vector if not properly secured.

* **Usage:** IT administrators use RDP to manage servers and desktops without needing physical access to the machine.
* **Risks:** RDP is often targeted by attackers due to its direct access to systems. If exposed to the internet with weak credentials or outdated configurations, it becomes vulnerable to brute force and credential-stuffing attacks.
* **Mitigation:** Using strong, unique passwords, enabling multi-factor authentication (MFA), restricting access with firewalls, and monitoring RDP logs for unusual activity.

## Brute Force Attacks

A brute force attack involves systematically trying multiple username and password combinations to gain unauthorized access to a system. Attackers use automated tools to rapidly attempt various credentials until they find a match, exploiting weak or reused passwords.

* **Common Targets:** RDP, SSH, web applications, and other services requiring authentication.
* **Detection:** Monitoring failed login attempts, detecting abnormal spikes in authentication requests, and setting up alerts for unusual login patterns.
* **Prevention:** Account lockout policies, IP whitelisting, rate limiting, and using tools like Fail2Ban to block suspicious IP addresses.

### RDP Brute Force Attack Using Crowbar

In our lab, we simulated an RDP brute force attack on the Windows server using Crowbar, a brute force tool capable of attacking various remote authentication services.

* **Crowbar Attack Execution:**
    * The attacker, using a Kali Linux machine, launched Crowbar to test multiple password combinations against the Windows server's RDP service.
    * The attack was aimed at identifying weak or easily guessable credentials.

Example command to launch Crowbar against the RDP service:

    ```bash
    crowbar -b rdp -s <Windows_Server_IP> -u <username> -C /path/to/password_list.txt
    ```

    Note: You can add your windows server password on your attack wordlist just for fun.

* **Outcome:** The attack generated multiple failed login attempts, which were logged and forwarded to the Elastic Stack via the Elastic Agent. The failed logins appeared in Kibana dashboards, making it easy for the SOC analyst to spot the brute force pattern and take action.

## Dashboards in Elasticsearch
Dashboards are a powerful feature in Elasticsearch, providing visual insights into the collected data through charts, tables, and graphs. In a SOC environment, dashboards help analysts quickly spot anomalies, investigate security events, and correlate data from various sources.

* **Purpose:** Dashboards offer a centralized view of security events, showcasing login attempts, suspicious activities, and system health.
* **Creation:** Using Kibana, you can create custom visualizations by querying Elasticsearch data and organizing the visualizations into a dashboard layout.

### Example Queries for Dashboard Creation

In my project, I built dashboards using specific queries to monitor authentication events and detect suspicious activity:

![Dashboard-On-SSH-Activities-On-Endpoint](https://github.com/user-attachments/assets/3c97328a-5b79-4931-bf7b-1ae85b0e1bdd)

* **Failed SSH Login Attempts:**

    ```
    system.auth.ssh.event : * and agent.name: MYDFIR-Linux-collinscurtis and system.auth.ssh.event: Failed
    ```

* **Successful SSH Logins:**

    ```
    system.auth.ssh.event : * and agent.name: MYDFIR-Linux-collinscurtis and system.auth.ssh.event: Accepted
    ```

![Dashboard-On-RDP-Activities-On-Endpoint](https://github.com/user-attachments/assets/45bbc6bf-35be-484b-b5b9-85b0ff1babcf)

* **Failed RDP Login Attempts (Windows Event ID 4625):**

    ```
    event.code : 4625 and agent.name: MYDFIR-WIN-collinscurtis
    ```

* **Successful RDP Logins (Windows Event ID 4624, Logon Types 10 and 7):**

    ```
    event.code : 4624 and winlog.event_data.LogonType : 10 or winlog.event_data.LogonType : 7
    ```

These queries allow you to visualize authentication trends, spot brute force attempts, and identify successful intrusions, giving analysts the context they need to take timely action.

## Command and Control (C2)

Command and Control (C2) is a technique used by attackers to remotely manage compromised systems within a target network. After gaining initial access, attackers use C2 servers to issue commands, gather data, and maintain persistent access. C2 infrastructure is a critical component of advanced persistent threats (APTs) and red team operations.

* **How C2 Works:**
    * The compromised machine ("beacon") connects to the C2 server.
    * The C2 server sends instructions (e.g., run commands, escalate privileges, exfiltrate data).
    * The beacon executes the commands and returns the results.

In this project, we set up a Mythic C2 server to simulate real-world attack scenarios.

### Installing Mythic on Ubuntu Linux

Mythic is an open-source C2 framework that provides a modular, flexible, and intuitive platform for red teaming. Here's a simplified installation process:

1. **Update System Packages:**

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

2. **Install Required Packages:**

    ```bash
    sudo apt install docker.io docker-compose -y
    ```

3. **Clone Mythic Repository:**

    ```bash
    git clone [https://github.com/its-a-feature/Mythic.git](https://github.com/its-a-feature/Mythic.git)
    cd Mythic
    ```

4. **Configure and Start Mythic:**

    ```bash
    sudo ./mythic-cli install
    sudo ./mythic-cli start
    ```

5. **Access the Mythic Web Interface:**

    Open a browser and navigate to `http://<your-server-ip>:7443` to log in and start managing agents.

![Mythic-C2](https://github.com/user-attachments/assets/397c0f4d-82ae-44d5-a3dd-fbe8f87f510a)

The image above is a mythic c2 server which will be our command and control center.

## Alerts in ELK

Alerts are an essential feature in any SOC environment, enabling analysts to detect and respond to suspicious activities in real-time. In Elasticsearch, alerts are triggered by specific rule-based conditions, helping analysts stay on top of potential threats without manually sifting through endless logs.

* **What Are Alerts?**

    Alerts are automated notifications generated when specific events or patterns are detected in log data. They help SOC analysts rapidly identify threats, investigate incidents, and take immediate action to mitigate attacks.

* **Why Alerts Are Helpful for SOC Analysts:**
    * **Early Threat Detection:** Catch suspicious activities like brute force attempts or malware execution as they happen.
    * **Faster Incident Response:** Enable analysts to respond quickly, reducing the time attackers have to establish persistence.
    * **Efficient Monitoring:** Automate log analysis, freeing up analysts to focus on more complex investigations.
    * **Customizable Rules:** Tailor alerts to the environment’s specific security needs and threat landscape.

* **Creating Alerts in ELK:**

    In Kibana, you can create alerts by defining detection rules. These rules query log data, searching for specific event patterns. When a match is found, an alert is triggered, which can then notify analysts via email, Slack, or other communication channels.

* **For guidance on setting up alerts, check out these helpful YouTube videos:**
    * [How to Create Alerts in ELK - Part 1](https://www.youtube.com/watch?v=11eBIfDeZ7k)
    * [How to Create Alerts in ELK - Part 2](https://www.youtube.com/watch?v=pAfIi6Z6a2g)

### Example Alert Rules

In my project, I implemented several alert rules to catch different types of threats:

* **SSH Brute Force Attempt:**

    Triggered when multiple failed SSH login attempts to the root user are detected on the Linux server.

    ```
    system.auth.ssh.event : * and agent.name : "MYDFIR-Linux-collinscurtis" and system.auth.ssh.event : "Failed" and user.name:"root"
    ```

    ![SSH-Brute-Force-Alert-Rule](https://github.com/user-attachments/assets/75bdfd77-81d6-4608-89df-4c0e5a3cce35)

* **RDP Brute Force Attempt:**

    Detects repeated failed RDP login attempts to the Administrator account on the Windows server.

    ```
    event.code : "4625" and agent.name : "MYDFIR-WIN-collinscurtis" and user.name : "Administrator"
    ```

    ![RDP-Brute-Force-Alert-Rule](https://github.com/user-attachments/assets/fb1d845a-9bd6-4344-ad5e-ef62eeb3b3fa)

* **Mythic C2 Apollo Agent Detected:**

    Flags events indicating the presence of a Mythic Apollo agent on a Windows endpoint, based on file hash and executable name.

    ```
    event.code : "1" and (winlog.event_data.Hashes: "F8A9CA51734A8B7ACE33F2961705A162643813C3D569FBB27316483C1EF4E81B" or winlog.event_data.OriginalFileName : "Apollo.exe")
    ```

    ![Mythic-C2-Agent-Alert-Rule](https://github.com/user-attachments/assets/23876cd0-f9f2-46c6-8c97-e8199796c055)

These alert rules empower SOC analysts to detect attacks and suspicious activity, providing the visibility needed to secure the environment effectively.

## Attack Diagram

The attack diagram outlines a multi-phase attack chain, demonstrating different stages of an adversary’s approach to compromising a system.

![Attack-Diagram drawio](https://github.com/user-attachments/assets/d59183ea-e727-4674-b013-64beedd47d75)

This structured attack flow helps illustrate how various tactics are detected and logged within the ELK stack for later analysis.

* **Phase 1: Initial Access** — The attacker brute forces RDP credentials to access the Windows server. Upon successful authentication, they establish an initial foothold.
* **Phase 2: Discovery** — After gaining access, the attacker performs reconnaissance commands like `whoami`, `ipconfig`, and `net user` to gather information about the system and its users.
* **Phase 3: Defense Evasion** — The attacker disables security mechanisms (e.g., Windows Defender) to avoid detection.
* **Phase 4: Execution** — The attacker executes payloads via PowerShell to deploy the Mythic C2 agent, establishing persistent command and control.
* **Phase 5: Command and Control** — The C2 agent communicates with the Mythic server, allowing the attacker to issue remote commands and maintain control over the compromised machine.
* **Phase 6: Exfiltration** — The attacker simulates data theft by creating and downloading a fake password file.
The purpose of these simulated attacks is not only to test defensive capabilities but also to generate valuable log data for analysis and continuous improvement of the SOC environment. Any type of attack can be simulated, depending on the learning objectives — whether it’s privilege escalation, lateral movement, or data exfiltration, the goal is to create realistic logs and use them to refine detection and response strategies.



Below is an image of successful deployment and execution of my attack payload to my windows target system from my mythic c2 server.
![Payload-Deployed](https://github.com/user-attachments/assets/f67b3ec1-9aa7-4fb6-a1b7-915fe886d358)





## Investigations

In a Security Operations Center (SOC), investigations are a critical aspect of incident response. When an alert is triggered, SOC analysts must quickly assess the situation, determine the threat level, and decide on the appropriate course of action. This section outlines investigation strategies, key questions to ask, and best practices for handling incidents using a Security Information and Event Management (SIEM) system.

### Investigation Process

#### Alert Triage:
- **Review the alert details** (source, event codes, timestamps).
- **Cross-check with threat intelligence sources** (e.g., GreyNoise, AbuseIPDB) to see if the IP is flagged as malicious.

#### Context Building:
- Gather related logs to build a timeline.
- Check for other events tied to the same IP, user, or host.

### Key Questions to Ask:

#### SSH Brute Force Alert:
- **Is the IP recognized for brute force or other malicious activity?**
- **Are there multiple failed login attempts within a short time?**
- **Were any logins successful? If so, what actions followed the login?**

**Example:**
- **IP:** 218.92.0.155  
- **Malicious?** YES *(GreyNoise: Malicious, AbuseIPDB: 100% Confidence)*  
- **Affected Users?** Only root  
- **Successful Logins?** NO  

#### RDP Brute Force Alert:
- **Is the IP known for brute force attacks?**
- **Are multiple user accounts targeted?**
- **If successful, what processes or connections were made post-login?**

**Example:**
- **IP:** 111.92.61.249  
- **Malicious?** YES *(GreyNoise: Suspicious, AbuseIPDB: Not Listed)*  
- **Affected Users?** Administrator, admin  
- **Successful Logins?** NO  

### Writing an Investigation Report

#### Summary:
- A brief description of the incident and timeline.

#### Findings:
- Key observations from the logs and threat intel sources.

#### Impact:
- Which systems or users were affected?
- Was any data exfiltrated or modified?

#### Recommendations:
- Immediate actions *(e.g., block IP, disable compromised accounts).*
- Long-term improvements *(e.g., stronger password policies, improved logging).*

### Escalation & Post-Investigation

#### Escalate to SOC Managers:
- If a threat is active or critical systems are affected.

#### Documentation & Lessons Learned:
- Update playbooks based on the incident.
- Refine alerting rules to catch similar attacks earlier.

---

Below are images of alerts received throughout multiple days of testing and other outsider attempts to attack SSH and RDP sessions.

![Alerts-Based-On-Rules](https://github.com/user-attachments/assets/67fe8e52-eb57-47c5-96ea-c3b372340938)

![ELK-Alerts-Based-On-Rules](https://github.com/user-attachments/assets/61a30dd8-eac0-4f81-bcbc-774be98a032a)



## Ticketing System in SOC Environments

In a Security Operations Center (SOC), a ticketing system is a critical component for tracking, managing, and documenting security incidents and alerts. It serves as the backbone of incident response, ensuring that potential threats are systematically addressed and properly recorded for future reference and learning.

### What is a Ticketing System?

A ticketing system is a tool that logs events, issues, or alerts as individual records called tickets. Each ticket contains detailed information about the incident, including:

- **Incident Description:** A summary of the alert or issue.
- **Severity Level:** The urgency of the incident.
- **Event Logs & Evidence:** Related log entries or system artifacts.
- **Assigned Analyst:** The team member handling the case.
- **Resolution Status:** Tracks the progress of the investigation — from open to resolved.

### How SOCs Use Tickets

SOC analysts rely on tickets to structure their workflow. When an alert is generated in the ELK stack, for example, it can automatically trigger a ticket via webhooks. The ticket guides the analyst through the investigation process, ensuring key questions are answered (like IP reputation, affected users, and post-compromise activities). Once resolved, the ticket serves as historical documentation for threat trends and helps refine detection rules.

### Why Choose osTicket?

We selected **osTicket** as our ticketing system due to its simplicity, open-source nature, and seamless integration capabilities. It’s lightweight, easy to deploy, and supports webhook-based automation — perfect for pairing with ELK.

### Setting Up osTicket and Integrating with ELK

To set up osTicket and link it to ELK, these tutorials provide step-by-step guidance:

- **[osTicket Setup](https://youtu.be/xgxQuLL33oU?si=oW2muxktbnxHaLX-)**
- **[osTicket + ELK Integration](https://youtu.be/P9YxutqWAF0?si=u6V1kilYcJlgYYl_)**

This setup ensures that no security event goes unnoticed — enabling SOC analysts to respond swiftly and maintain a structured incident response process.

### Successful osTicket Deployment

Below are images of successful installations and integration of the osTicket server with ELK:

![osTicket-Installation](https://github.com/user-attachments/assets/bf303890-e98d-461e-a13e-cc79ca97654d)

![osTicket-Completed-Installation](https://github.com/user-attachments/assets/a9b26866-24da-4178-9732-d3bceed601aa)

![Ticketing-System](https://github.com/user-attachments/assets/11fd231c-b722-4ab9-ad39-49ce28e2d070)




## Elastic Defend (EDR)

Elastic Defend is a powerful security solution within the Elastic Security suite, designed to provide endpoint detection and response (EDR) capabilities. Built on the Elastic Stack, it allows organizations to detect, investigate, and respond to security threats in real time, leveraging advanced analytics and a vast threat intelligence database. Elastic Defend integrates seamlessly with other components of the Elastic ecosystem, making it a robust choice for Security Operations Centers (SOCs) aiming to enhance their monitoring and defense capabilities.

### Key Features of Elastic Defend

- **Real-Time Threat Detection:** Continuously monitors endpoint activities, detecting suspicious behaviors and known attack patterns using pre-built detection rules and machine learning models.
- **Endpoint Visibility:** Provides deep visibility into processes, file events, registry changes, and network connections, enabling SOC analysts to gain a detailed view of endpoint activity.
- **Automated Response:** Can automatically take remediation actions, such as isolating an infected host, stopping malicious processes, or deleting harmful files, reducing the response time to incidents.
- **Threat Hunting:** Allows analysts to perform proactive threat hunting using the Kibana interface, querying historical and real-time data to uncover hidden threats.
- **Customizable Rules:** Users can create custom detection rules tailored to their environment, enabling fine-tuned alerting for specific threats or suspicious activities.

### Deployment and Integration

Deploying Elastic Defend involves installing the Elastic Agent on endpoint devices, which serves as the data collector and security sensor. The agent forwards security telemetry to the Elastic Stack, where it is processed, analyzed, and visualized in Kibana.

#### High-Level Installation Steps:

1. **Fleet Server Setup:** Configure a Fleet server to manage Elastic Agents centrally.
2. **Elastic Agent Installation:** Install and enroll the Elastic Agent on target machines.
3. **Enable Elastic Defend Integration:** In Kibana, add the Elastic Defend integration to the relevant agent policy. *(If Elastic Agents are already installed, simply enable Elastic Defend in the policy.)*
4. **Define Detection Rules:** Enable or create detection rules in Elastic Security.
5. **Monitor and Respond:** Use the Security app in Kibana to view alerts, investigate incidents, and initiate responses.

For an in-depth, step-by-step installation guide, you can refer to this helpful resource:  
- **[Elastic Defend Setup](https://www.elastic.co/guide/en/security/current/install-endpoint.html)**

### The Role of Elastic Defend in the SOC

Elastic Defend acts as the SOC's eyes and ears at the endpoint level. It enhances threat visibility, reduces the mean time to detect (MTTD) and respond (MTTR), and provides rich context for investigations. When combined with dashboards, alerts, and threat intelligence, it empowers analysts to make faster, more informed decisions.

Below is an image of Elastic Defend in action on a Windows server after simulating attacks using Mythic C2 payloads.

![Elastic-Defend-Integration](https://github.com/user-attachments/assets/014526fa-6239-4e28-9888-6ca05b9ab8d1)

### Added Value of Elastic Defend

One of the key benefits of integrating Elastic Defend is that it comes with its own set of additional detection rules and alerts. Enabling these rules enhances visibility and helps analysts automate responses to various types of threats.

Below are some of the additional alert rules added automatically by integrating Elastic Defend:

![Additional-Elastic-Defend-Detection-Rules](https://github.com/user-attachments/assets/0e1845a6-60e8-43c6-bd4f-c91f9d202790)

This added layer of defense strengthens an organization's security posture, empowering analysts to stay ahead of evolving threats with minimal manual intervention.





## Conclusion

This project encapsulates the essence of a modern Security Operations Center (SOC) by simulating real-world attack scenarios, monitoring threats through the Elastic Stack, and managing incidents with a ticketing system like osTicket. By carefully designing an environment that mirrors enterprise networks, we gained practical experience in threat detection, analysis, and response workflows.

The hands-on approach helped solidify concepts around adversary tactics, techniques, and procedures (TTPs), empowering us to build better defenses and refine incident handling strategies. Through simulated attacks like brute force RDP, C2 communications, and data exfiltration, we learned to configure alerts, investigate threats, and correlate events across multiple data sources.

One of the most significant takeaways is the ability to translate theoretical knowledge into practical skills. The project provides a solid foundation for more advanced cybersecurity pursuits, such as threat hunting, malware analysis, and even red team operations. As technology evolves, this environment can be continuously updated to test new attack vectors and refine detection rules.

Ultimately, this project serves as both a learning platform and a blueprint for building more robust and resilient security architectures. Whether you're an aspiring SOC analyst, a security researcher, or an experienced professional, the skills developed here are invaluable for tackling real-world cybersecurity challenges.











## Further Activities and Observations

Throughout the project, we extended our exploration by simulating more complex adversarial activities, capturing the resulting telemetry, and visualizing the attack data within the Elastic Stack. This section showcases these additional activities, explaining their significance and the insights they provide.

### RDP Brute Force Attack

![RDP-Brute-Attack](https://github.com/user-attachments/assets/d1bbf383-20e5-4133-adc7-1d25eb9e4656)

I initiated a brute-force attack against the Windows server using the **"crowbar"** tool just for Proof of Concept (PoC). The attacker systematically tried multiple credentials until successfully logging in with the username `Administrator` and the password `Summer2025!`. This event was captured in the logs and visualized in the Elastic dashboard, showing the source IP, target system, and timestamp of the successful authentication.

- **Significance:** Brute-force attacks are a common initial access technique. Capturing and visualizing these attempts helps analysts identify repeated failed logins and correlate them with other suspicious activities.

### Command and Control (C2) Operations

![Mythic-C2-Comms](https://github.com/user-attachments/assets/1b3bcdc3-287a-4e21-a7f6-0f56de3da8a5)

After gaining access, I deployed a **Mythic C2** agent to the compromised system. The agent connected back to the Mythic server, providing the attacker with remote command execution capabilities. Using the C2 channel, we listed directories, explored user documents, and eventually found and exfiltrated a file named `passwords.txt`.

- **Significance:** C2 operations simulate real-world post-exploitation scenarios. Monitoring process creations, network connections, and file access events helps detect and disrupt adversaries maintaining persistence within the environment.

### Dashboard Visualization

![Dashboard-On-Suspicious-Activities](https://github.com/user-attachments/assets/34a675d7-31f9-415f-b2f5-2a757dd02c61)

I further created Elastic dashboards to visualize the attack chain, displaying processes spawned, network connections initiated, and security tools disabled. For instance, we observed `svchost.exe` creating suspicious subprocesses, including `rundll32.exe`, used for stealthy payload execution.

- **Significance:** Visualizing telemetry data aids in threat hunting and forensic analysis. Analysts can spot anomalies, trace attack paths, and improve detection rules based on observed patterns.

These extended activities enriched the project, reinforcing the importance of continuous monitoring, log aggregation, and proactive threat detection. By generating real attack data and observing it through the lens of a SOC, we simulated the intricate dance between attackers and defenders, deepening our understanding of cybersecurity operations.

