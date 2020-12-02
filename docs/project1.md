# Potential Project Ideas

## [Cyberpatriot Vulnerable VM Labs](decomposition/mindmap.md)

### Topic Definition

This project would entail working with Duane Dunston to create intentionally vulnerable virtual machines for use by the Cyberpatriots community. Labs would aid in the education of high school students starting to learn about security.

### Overview

Research needs to be done into common vulnerabilities that exist on Linux and Windows systems and how remediations can be performed. This research would culminate into virtual machines or scripts that can be distributed to students. Alongside producing these virtual machines, lab guides must be created that document how to find the vulnerabilities that were introduced in the previous phase of the project. This project would be a great way to help bring elements of information security that we see at a collegiate level over to high school students to help shape their learning experience.

### Description

Vulnerabilities must be introduced into two different systems - Windows and Linux. Linux vulnerabilities could be introduced and then the virtual machine could be powered off, saved, and exported for use elsewhere due to a small size. Windows virtual machines are more complex to distribute at scale, and may require the use of a script that a student runs against their own virtual machine to introduce vulnerabilities. Lab guides detailing remediations should be clear and explained at a beginner level to clearly explain why these vulnerabilities are relevant.

&nbsp;

## Open Source Managed Services

### Topic Definition

Develop a solution for forwarding data from client SIEM devices to a managed security service provider. The goal of this project would to enable an analyst to easily work with client data and could allow threat intelligence against multiple organizations. 

### Overview

Client and service provider architecture needs to be set out to work with client data in a meaningful way. Additionally, this project could be extended to correlating data on different entities using the aforementioned system, giving a defender insight on attacker activities across multiple clients. This project could benefit small managed service providers who are seeking a way to correlate security data across multiple clients.

### Description

Architecture needs to be planned on how clients will send data to the service provider and the structure of the service provider itself. One possibility could be Elastic Stacks at clients that forward data into an [Apache Kafka](https://kafka.apache.org/) instance or a service provider [Logstash](https://www.elastic.co/logstash) instance. This could pull data into an overarching Elastic Stack for the service provider's use. From here, incidents could be managed with [The Hive](https://thehive-project.org/) for alert management and organization. For demonstration purposes, an alerting mechanism will need to be leveraged on networks being monitored. One possibility could be deploying [Kolide](https://www.kolide.com/fleet/) with [Osquery](https://osquery.io/) and developing or finding common rulesets to produce alert data.
