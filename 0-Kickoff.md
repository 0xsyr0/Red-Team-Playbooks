# General Questions

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
```
- Lockout threshold
- Lockout duration
- Lockout observation window
```

# PTK Related Questions

* Has the PTK been deployed yet? If not, can it be dropped at the latest final business day before we start with our assessment? This is necessary to ensure that no issues arising during the deployment.
* Does the PTK run on a laptop/workstation or in a vSphere environment?
* If deployed on a laptop/workstation, has the virtual NIC been configured to be in "Bridged Mode"?
* Dies the PTK have full access to all hosts in scope of the network?
* Is the PTK deployed on the same subnet as the employee clients?

# Onsite Related Questions

* On arrival to the site, should we immediately introduce ourselves to the receptionist? Or are we permitted to simply walk in, see if we are stopped, and if not trying to find a desk or open network port to start with initial testing?
* When onsite, are we permitted to interact with unlocked employee workstations?
* Will we be facing controls such as Cisco ISE or NAC? If yes - are we allowed to bypass these controls by moving around the building and searching for unsecured ports to hijack from other devices such as printers or phones?
* Can we test into the evening and after normal business hours?
* Is there any dress code? Usually we are going for the high end of their dress code unless we are doing some physical social engineering.
