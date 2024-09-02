# SOC Monitoring and Incident Response Implementation

## 1. Project Overview

This project focuses on the complete setup and implementation of a Security Operations Center (SOC) monitoring and incident response architecture within a Virtual Private Cloud (VPC) hosted on Vultr. The architecture involves configuring and deploying various security tools and components, including Elastic & Kibana for log aggregation and real-time monitoring, osTicket for incident management, and managed servers (Windows and Ubuntu) that forward logs to the monitoring system.

Additionally, this setup simulates a realistic adversarial environment using an attacker's laptop running Kali Linux and a Command and Control (C2) server (Mythic) to facilitate red team exercises and incident response scenarios. This project is designed for practical applications in cybersecurity training, blue team defense, and red team offensive activities.

## 2. Project Components
![Architecture Diagram](https://github.com/user-attachments/assets/4105f4df-6d1e-43f9-8d29-7e2f7cfa78af)

### 1. SOC Analyst Workstation
- **Role:** The SOC Analyst uses this workstation to connect to the Elastic & Kibana dashboard via a web GUI over the Internet, monitoring network activities, investigating alerts, and managing incidents.
- **Technology Stack:** Secure VPN, Web Browser, Kibana Web GUI.

### 2. Elastic & Kibana Stack
- **Role:** Central log aggregation and visualization platform. Collects logs from all managed servers, processes them, and provides insights into network security. It also generates alerts based on log data, which are forwarded to the osTicket server.
- **Setup:**
  - Deploy on an Ubuntu server within the VPC.
  - Install and configure Elasticsearch and Kibana.
  - Enable necessary plugins for alerting and reporting.
  - Configure data ingestion pipelines from the managed servers.
- **VPC Details:**
  - **Private Network:** `172.31.0.0/24`
  - **IP Range:** `172.31.0.1-254`
  - **Subnet Mask:** `255.255.255.0`

### 3. osTicket Incident Management
- **Role:** Manages security incidents by receiving alerts from Elastic & Kibana, allowing SOC analysts to track and resolve incidents effectively.
- **Setup:**
  - Deploy on an Ubuntu server within the VPC.
  - Configure to receive alerts and generate tickets from Elastic & Kibana.
  - Customize workflows for incident response procedures.

### 4. Managed Servers (Windows & Ubuntu)
- **Role:** These servers simulate an enterprise environment and are configured to forward system and application logs to Elastic & Kibana.
- **Setup:**
  - **Windows Server:**
    - Enable RDP for management.
    - Install and configure the Elastic agent to forward logs.
  - **Ubuntu Server:**
    - Enable SSH for secure access.
    - Install and configure Filebeat and Metricbeat to send logs to Elasticsearch.

### 5. Fleet Server
- **Role:** Centralized management for deploying and updating Elastic agents on managed servers.
- **Setup:**
  - Deploy on a dedicated server within the VPC.
  - Configure to manage agents on Windows and Ubuntu servers.

### 6. Attack Laptop (Kali Linux)
- **Role:** Used by the red team to simulate attacks on the network. These attacks are logged and monitored by the SOC to test and refine their response capabilities.
- **Setup:**
  - Deploy Kali Linux within the VPC or on a separate network segment.
  - Simulate various network attacks like phishing, brute-force, or exploitation.

### 7. C2 Server (Mythic)
- **Role:** Command and Control (C2) server used by the attacker to manage compromised systems, deploy payloads, and execute attacks remotely.
- **Setup:**
  - Deploy Mythic on a dedicated server within the VPC.
  - Configure Mythic for communication with compromised systems.

## 3. Implementation Plan

### 1. VPC and Network Configuration
- **Objective:** Set up a secure VPC on Vultr to host all components.
- **Steps:**
  - Create a new VPC with the specified IP range.
  - Deploy all required servers (Elastic & Kibana, osTicket, Windows, Ubuntu, Fleet, Kali Linux, Mythic).
  - Configure security groups to control access between components.

### 2. Deployment of Core Components
- **Objective:** Deploy and configure Elastic & Kibana, osTicket, and Fleet Server.
- **Steps:**
  - Install and configure Elasticsearch and Kibana on the designated server.
  - Set up osTicket for incident management.
  - Deploy and configure the Fleet Server for agent management.

### 3. Log Forwarding and Monitoring Setup
- **Objective:** Ensure all logs from managed servers are forwarded to Elastic & Kibana.
- **Steps:**
  - Install and configure Elastic agents on Windows and Ubuntu servers.
  - Set up log forwarding rules and data pipelines in Kibana.
  - Configure alerting rules based on log patterns.

### 4. Simulation of Adversarial Environment
- **Objective:** Deploy and configure the attacker’s environment to simulate real-world attacks.
- **Steps:**
  - Set up the Kali Linux attacker's laptop and Mythic C2 server.
  - Simulate various attacks (e.g., phishing, brute force, exploitation).
  - Monitor and analyze logs and alerts generated by these attacks in Kibana.

### 5. Incident Management Workflow
- **Objective:** Integrate incident management into the SOC workflow.
- **Steps:**
  - Customize osTicket to create workflows that match the organization’s incident response plan.
  - Test the incident response process using simulated attacks.
  - Train SOC analysts on handling incidents using the new setup.

## 4. Project Use Cases

### 1. Blue Team Activities
- Monitor network activity in real-time, detect anomalies, and respond to threats using Elastic & Kibana.
- Track and resolve incidents efficiently through osTicket.

### 2. Red Team Exercises
- Simulate cyberattacks using the Kali Linux attacker’s machine and Mythic C2 server.
- Test the SOC’s ability to detect, analyze, and respond to attacks.

### 3. Training and Development
- Provide hands-on experience for SOC analysts in log monitoring, threat detection, and incident management.
- Conduct drills and scenario-based training exercises.
