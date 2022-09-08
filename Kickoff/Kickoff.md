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

* What is the Red Team
* What is the job of the Red Team
* Why this scope has been chosen
* What is the mission objective
* What are we setting out to archive or to demonstrate?
* How the assessment will spun up

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

* <ASSESSMENT_NAME>
	* Tickets
	* Scope
		* Internal
		* External
	* Trust Agents
	* Duration and Time Slots
	* Personally Identifiable Information (PII)
	* Notification Requrements
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

* Has the PTK been deployed yet? If not, can it be dropped at the latest final business day before we start with our assessment? This is necessary to ensure that no issues arising during the deployment.
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

### Next
- [Operations](https://github.com/0xsyr0/Red-Team-Playbooks/blob/master/Operations/Operations.md)
