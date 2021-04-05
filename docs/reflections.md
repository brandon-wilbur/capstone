# Week 2 Reflection

During this period, we communicated with Duane and Devin and ironed out our reporting schedule for the semester for the stages of our project. We're going to continue our previous model but start with one deliverable every three weeks, ending with a meeting with Duane and Devin to discuss our progress. At this time, I am going to continue working on Windows labs and Ryan is going to work on Linux. We came up with a list of possible lab ideas that weren't yet touched upon from last semester:

* password hardening
* Apache vulnerabilities
* phpMyAdmin vulnerabilities
* SSH key permission misconfiguration
* Cisco Packet Tracer
* Nirsoft CurrPorts network / process enumeration
* Scheduled tasks and services
* Cronjobs
* Mounted media

At this point, I have started to work on a lab using Nirsoft CurrPorts to identify a vulnerable Windows Virtual Machine, and Ryan is focusing on Cisco Packet Tracer labs. These two were identified by Duane as priority items that teams would like to work with. We also discussed the possibility of working with teams directly and presenting content to interested students. Work on the project so far has continued as usual and feels on par with last semester's tempo.

# Week 3 Reflection

During this week, I made significant headway on the lab guide due this week. I completely ironed out the Ncat backdoor to be installed on the infected machine. In order to create more noise and more content to cover in the lab, I wanted to add at least one more backdoor. I ended up using msfvenom to create a Windows TCP bind backdoor. In order to deliver this in a script, I tried to Base64-encode the binary's data and store it in the script, but Windows Defender will block PowerShell scripts with the plain Base64-encoded data within. Another layer of obfuscation through Gzip proved unsuccessful, so I eventually turned to using the Invoke-Obfuscation utility. This is a publicly available PowerShell script that can compress entire scripts, but I'm leveraging it to store the malicious PE file within my PowerShell script. 

Additionally, Nirsoft CurrPorts was successfully installed and could be used to identify all network connections and binaries associated with those connections. WinRM was also enabled to demonstrate listening on additional ports. The sprint meeting is set for Friday February 19th where the script must be completed and the lab guide must be finished.

Progress made:
* Invoke-Obfuscation utility for obfuscation of malicious script content
* msfvenom to create TCP bind backdoor
* Ncat backdoor configured
* WinRM enabled

To do:
* Test TCP bind backdoor and make it persistent
* Test installing TCP bind backdoor as a service
* Install noisy network programs
* Lab Guide documentation

# Week 4 Reflection

During this week, I finished the PowerShell script for the lab and completed the lab guide. I ended up implementing 3 different backdoors: one TCP bind meterpreter shell, and two netcat shells. Two of these were installed as services, and one was set to run on startup under privileges of `NT AUTHORITY\SYSTEM` as a scheduled task. This provided opportunities in the lab guide to discuss processes, services, and networking on Windows. 

In the lab guide, a lot of time was devoted to explaining processes, users, and a bunch of different related attributes that are built-in and what should be expected on a Windows system. Throughout the lab, I referenced CurrPorts, Process Explorer, and Autoruns. This helped describe process relationships, privileges, and locations of PE files and how they relate to running processes. Our presentation of this sprint's progress went well and the amount of work completed this sprint will serve as a good baseline for our next sprint's work.

# Week 5 Reflection

This week, I reached out to Duane on system hardening resources. I've started to go over CIS standards and think about what I can create for the next lab. Duane taught a system hardening course last semester and I will be using some resources he created to build into a lab guide into generic Windows system hardening. This next week will consist of more research and finalizing a list of points that are going to be touched upon in the lab so the PowerShell script can be focused on introducing vulnerabilities in specific areas.

# Week 6 Reflection

This week, I finalized the list of topics that I'm going to be covering in the lab and reviewed Duane's resources on Windows hardening:

## Topics:

* Local Security Policies
    * `net accounts` to view current policies in place
    * use `Local Security Policy` editor to modify policies on local system in GUI, use `Explain` tab for setting description.
        * `Security Settings > Account Policies > Password Policy`
            * modify password requirements for users
        * `Security Settings > Account Policies > Account Lockout Policy`
            * modify lockout settings for users
        * `Security Settings > Local Policies > Audit Policy`
            * change what events are audited (logs) for various events regarding users / privileges
        * `Security Settings > Local Policies > User Rights Assignment`
            * disable RDP logon
            * specify who can log on locally
        * `Security Settings > Local Policies > Security Options`
            * don't display username at login
            * give user warning before password expiration
            * rename Administrator account
            * rename Guest account
            * add interactive logon message title and message
* Run `net user <username> *` to change the local password of an account
* Run Windows Update locally
* WSUS for domain organizations
* Windows Defender
    * `Windows Security > Virus & threat protection settings`
        * enable Real-time protection
            * Demonstrate PowerShell reverse shell one-liner failing
        * enable Cloud-delivered protection
        * automatic sample submission (off for corporate environments, explain sending data to Microsoft)
        * controlled folder access
            * Requires Win 10 Pro or Win 10 Enterprise
            * Demonstrate [ransomware test script](https://thomasrayner.ca/using-powershell-to-simulate-a-ransomware-attack/)
        * audit exclusions
    * `Windows Security > Firewall & network protection`
        * Turn the Firewall on
    * `Windows Security > App & browser control`
        * Audit settings for Edge and Internet Explorer
    * `Windows Security > Device security > Core isolation`
        * turn on memory integrity

In addition, CIS benchmarks need to be reviewed before creating the lab guide this week. I plan on scanning these and identifying easy wins to include in the lab that align with what material Duane covered so far.

# Week 7 Reflection

This week was crunch time for the second sprint with hammering out documentation. The above points were implemented in the PowerShell script. After configuring policies in the local security policy editor, the configuration was exported into a file and then converted to a Base64 string. When the script runs, this poorly-configured policy will be dropped to disk to be applied and then removed. Additionally, UAC bypass was configured to touch on an additional element of system hardening. After the lab is complete, the lab guide may be a good time to discuss the Windows Event log and show the benefits that Sysmon can provide.

# Week 8 Reflection

This week was a light week on project work, but I made a helper script with a custom PowerShell function, `Set-LocalSecurityPolicy`, to help future developers of this project produce more diverse local security policies per Duane's request. Our second sprint officially ended on Monday, so this third sprint will be focused on unnecessary software on a Windows system. Because this is anticipated to be lighter than usual, this sprint is going to also focus on an organization system for this project. This can easily live inside a GitHub repo with Github Pages used for presentation. This will easily allow anyone who wants to contribute to submit their own markdown files for new labs and scripts can be easily linked here. Some work needs to be done to convert our current Word documents into markdown so it can more easily live here. In addition to this, we're going to need to add some documentation to explain clearly what each lab is trying to demonstrate so information is easier to find.

# Weeks 9-11 Reflection

In this cycle, I focused on creating a software auditing lab for unneeded software on Windows 10. This required finding software to install and then remove from Windows 10 using Chocolatey and optional features in Windows. I ended up using OpenSSH and Hyper-V as different pieces of software for the user to install. On top of this, I showed how to configure Bitlocker and restrict the software that users of a workstation could run. This wasn't demonstrable on my workstation due to licensing not meeting the criteria to run Bitlocker, but steps should prove successful on a legitimate copy of Windows 10 used on a virtual machine.

In addition to this, a main focus of this sprint was getting our capstone project organized and presentable. Ryan and I decided that the project would be most easily accessible and open to future contributions on GitHub. While it is still a work in progress, we launched a repo under my account at this link:

<https://github.com/brandon-wilbur/cyberlabs>

And the presentable GitHub page was published at this link:

<https://brandon-wilbur.github.io/cyberlabs/>

Ideally, this can be used as an open location for any volunteers to publish lab content. Underlying markdown files and all items lying in the `/docs` directory of our repo make it relatively simple for any individual to fork our project and submit a pull request to add more content. We chose to stick with the name **Cyberlabs**, as the content contained within here can stretch more broadly beyond just the CyberPatriot program for which the guides are originally intended. Rather than writing labs in Word and distributing them with a semi-public Google Drive link, anyone can distribute our guides with a simple URL to any interested parties. I am very satisfied at the overall look and organization of our labs in this current state and will get feedback from Duane and Devin tomorrow.