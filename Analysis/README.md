# Analysis

Example alert:
Alert: Network - Inbound Cobalt Strike IP Detected
Time: 2024-01-10 04:10:10 UTC
Source: 40.194.28.30
Destination: 172.28.92.7
TCP Flag: SYN

First you want to understand the alert. You should start by asking yourself some questions:
- Why did this alert trigger?
- What were the conditions?
- How was the alert created?
- Why is the alert looking for this?
- What phase in the MITRE ATT&CK might this be in?
- What is the fidelity of this alert? (Advanced)

By asking yourself these questions, you can begin to identify the purpose and learn more about the criteria for this alert, which will then allow you to start questioning the validity of the alert. Asking yourself why the alert triggered can help you come up with objectives before diving into the logs. 

For example, this alert is looking for Cobalt Strike activity as it's a popular exploitation tool used by adversaries. Now your objective can be to look for processes that are estblishing outbound connectuions towards this particular external IPs. And if found, may indicate the possible usage of Cobalt Strike. 
