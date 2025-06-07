# Kickoff

## Table of Contents

- [Introduction](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#introduction)
- [Standard Operation Procedure (SOP) Checklist](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#standard-operation-procedure-sop-checklist)
	- [Preparation](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#preparation)
	- [Execution](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#execution)
	- [Wrap up](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#wrap-up)
- [Kickoff Meeting](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#kickoff-meeting)
	- [Structuring](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#structuring)
- [General Questions](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#general-questions)
- [Penetration Testing Kit (PTK)](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#penetration-testing-kit-ptk)
- [Onsite](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md#onsite)

## Introduction

### What is a Red Team?

- Adversary Emulation
- Adversary Simulation
- Social Engineering
- Tabletop Exercises or Wargaming

### Questions and Clarification for the Customer

* What is the job of the Red Team
* Why this scope has been chosen
* What is the mission objective
* What are we setting out to archive or to demonstrate?
* How the engagement will spun up

### Why performing red team engagements and adversary emulations?

- Obtain a holistic view of organization's information security posture
	- Not just a "limited scope" assessment
	- To answer the question "Can this breach/attack happen to us?"
- Cognitive Bios
- Measure people, process and technology
- Test assumptions
- Train and improve the blue team

### Test People, Process, and Technology

- Record all actions and times
	- To obtain initial access/patient zero
	- To move laterally from system to system
	- To identify, detect, and/or alert on each TTP
	- To escalate events into incident
	- To contain each host and eradicate malware
- Observe and document processes
	- From SOC to incident handling to hunting, logs help with deconfliction
	- Communications and alert to leadership of attack

### Focus on Stealth

- The red team is focused on testing detection and response
- Getting caught is okay, just make sure it's on you own terms
- Mature red teams
	- Know their tools and the footprints they leave behind
	- Track and clean indicators of compromise
	- Maintain operational security throughout the engagement
	- Ensure that all actions are measured and deliberate

### Frameworks

- Cyber Kill Chain Lockheed Martin
	- Unified Cyber Kill Chain: Paul Pols
- MITRE ATT&CK
- Purple Team Exercise Framework (PTEF)

### Infrastructure

#### Command & Control Communication Channels

##### Most popular C2 channels

- HTTP/S (network egress)
- DNS (network egress)
- TCP (peer-to-peer)
- SMB (peer-to-peer)

##### Esoteric C2 channels

- Gmail
- Google Drive
- Slack
- Twitter
- DNS-over-HTTP

##### Command & Control Controll Tiers

Tier 3: Intertactive (regular ops)
Tier 2: Short Haul (short-term) (longer callback than tier 3, callback every few hours)
Tier 1: Long Haul (long-term) (maintaining access, callback > 24/48 hours)

Get in with tier 3 than migrate to tier 2 and kick of your tier 3 and after that hop on to tier 1 and kick off your tier 2.

##### OPSEC

- Short and Long Haul
- Functional Segregation
- Redirectors

##### Rules

- Only use a specific tier for its intended purpose
- Use unique profiles of each tier, ensure a variety of communication types
- Increase sleep timers when not in use
- Hand off sessions down but not up the tier model
- The higher the tier, the higher likelihood compromise but the faster the callback cycle

##### Long Haul vs. Short Haul

- Interactive: High risk, fastest callback cycles
- Short Haul
	- Uses callbacks for communication
	- Used as a backup to re-establish interactive sessions
	- Commonly 1-24-hour callback cycles
- Long Haul
	- Uses callbacks on much longer intervals, greater than 24 hours
	- Designed to be slow and well blended for regaining lost control
	- Persistence mechanisms call back to long haul servers
	- Highest value servers, losing a long-haul server might end the entire engagement

#### Functional Segregation

- Consider segreating these functions on different assets
	- Phishing SMTP
	- Phishing payloads
	- Long-term C2
	- Short-term C2
- Each of these functions will likely be required for each social engineering campaign
- Since active incident response is typical in a red team engagement, a new set of infrastructure should be established each campaign

### Standard Operation Procedure (SOP) Checklist

#### Preparation

* Attack Plan
* Objectives
* Stakeholders
* Targets
* Timelines and Duration
* Planned Activities
* Risk Management
* Authorization
* Notification

#### Execution

* Work Towards Objectives
* Scanning
* Attacks
* Tactics, Techniques, Procedures (TTP)
* Documenting Activity and Logs
* Defects and Incidents
* Status Updates
* Syncs and Triage Meetings

#### Wrap Up

* Clean-Up
* Archival
* Eviction Support
* Summary
* Debrief
* Reports
* Reflect

## Kickoff Meeting

### Structuring

* <ENGAGEMENT_NAME>
	* Tickets
	* Scope
		* Internal
		* External
	* Trust Agents
	* Duration and Time Slots
	* Personally Identifiable Information (PII)
	* Notification Requirements
	* Rules Of Engagement (ROE)
	* Tools, Techniques and Procedures (TTP)
	* Goal
	* Measures of success/failure
	* Emergencies

## General Questions

* Ensure all questionnaire information has been completed.
* If all in-scope IP addresses have been provided:
	* Double check if the provided IP addresses are really in scope! Especially when they provide subnet ranges (i.e. 10.0.0.0/24)
	* Are any systems are legacy or fragile systems which may need additional care to preserve uptime?
	* Does the target systems contain, store or process any PII or PCI data?
	* Does the network have any segmentations that we should aware of?
* Will a valid domain user account be provided for testing, simulating the initial compromise of a single employee's credentials/workstation?
* What is the biggest priority in protecting?
* What is the account lockout policy? If we should encounter a login interface and attempt password spraying attacks, we would like to avoid causing lockout distruptions.

* From the lockout policy we need the following informations:

```c
- Lockout threshold
- Lockout duration
- Lockout observation window
```

## Penetration Testing Kit (PTK)

* Has the PTK been deployed yet? If not, can it be dropped at the latest final business day before we start with our engagement? This is necessary to ensure that no issues arising during the deployment.
* Does the PTK run on a laptop/workstation or in a vSphere environment?
* If deployed on a laptop/workstation, has the virtual NIC been configured to be in "Bridged Mode"?
* Dies the PTK have full access to all hosts in scope of the network?
* Is the PTK deployed on the same subnet as the employee clients?

## Onsite

* On arrival to the site, should we immediately introduce ourselves to the receptionist? Or are we permitted to simply walk in, see if we are stopped, and if not trying to find a desk or open network port to start with initial testing?
* When onsite, are we permitted to interact with unlocked employee workstations?
* Will we be facing controls such as Cisco ISE or NAC? If yes - are we allowed to bypass these controls by moving around the building and searching for unsecured ports to hijack from other devices such as printers or phones?
* Can we test into the evening and after normal business hours?
* Is there any dress code? Usually we are going for the high end of their dress code unless we are doing some physical social engineering.

### Previous

- [Kickoff](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Kickoff/Kickoff.md)

### Next

- [Operations](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md)
