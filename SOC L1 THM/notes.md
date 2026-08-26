# SOC LVL 1 ROOM THM 

## Introduction To SIEM (Security Information and Event Management)

Devices continuously generate logs of the activities that occur within them, those are also called log sources 

1) Host-Centric Log Sources

These log sources capture events that occurred within or related to the host. Devices that generate host-centric logs include Windows, Linux, servers, etc. Some examples of host-centric logs are:

A user accessing a file
A user attempting to authenticate.
A process execution activity
A process adding/editing/deleting a registry key or value.
PowerShell execution

2) Network-Centric Log Sources

Network-related logs are generated when the hosts communicate with each other or access the internet to visit a website. Devices that generate network-centric logs are firewalls, IDS/IPS, routers, etc. Some examples of network-centric logs are:

SSH connection
A file being accessed via FTP
Web traffic
A user accessing the company's resources through VPN.
Network file sharing Activity

=> The issue is that we can't analyse them without a SIEM 


Linux OS stores all the related logs, such as events, errors, warnings, etc. These are then ingested into SIEM for continuous monitoring. Some of the common locations where Linux stores logs are:

/var/log/httpd: Contains HTTP Request  / Response and error logs.
/var/log/cron: Events related to cron jobs are stored in this location.
/var/log/auth.log and /var/log/secure: Stores authentication-related logs.
/var/log/kern: This file stores kernel-related events.



## Alerting Process and Analysis 

### Use Case 1 
How do the SIEM triggers alerts ? Via detection rules 
Attackers are trying to remove logs post-exploitation phase to hide the tracks, but EVENT ID 104 every time a user tries to remove or clear event logs (if the rule is created ofc) 
=> We could create a rule as following ; **Rule: If the Log source is WinEventLog AND EventID is 104 - Trigger an alert Event Log Cleared**

### Use Case 2 
Adversaries use commands like whoami after the exploitation/privilege escalation phase. The following Fields will be helpful to include in the rule.

Log source: Identify the log source capturing the event logs
Event ID: Which Event ID is associated with Process Execution activity? In this case, Event ID 4688 will be helpful.
NewProcessName: Which process name will be helpful to include in the rule?
Rule: If Log Source is WinEventLog AND EventCode is 4688, and NewProcessName contains whoami, then Trigger an ALERT WHOAMI command Execution DETECTED


# Splunk : The basics 

## Splunk has 3 main components 

### Splunk Forwarder : Splunk Forwarder is a lightweight agent installed on the endpoint intended to be monitored, and its main task is to collect the data and send it to the Splunk instance.

### Splunk Indexer : Splunk Indexer plays the main role in processing the data it receives from forwarders. It parses and normalizes the data into field-value pairs, categorizes it, and stores the results as events, making the processed data easy to search and analyze.

### Search Data : Splunk Search Head is the place within the Search & Reporting App where users can search the indexed logs. He searches are done using the SPL (Search Processing Language), a powerful query language for searching indexed data. When the user performs a search, the request is sent to the indexer, and the relevant events are returned as field-value pairs.
