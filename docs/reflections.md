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