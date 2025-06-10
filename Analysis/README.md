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

For example, this alert is looking for Cobalt Strike activity as it's a popular exploitation tool used by adversaries. Now your objective can be to look for processes that are estblishing outbound connectuions towards this particular external IPs. And if found, may indicate the possible usage of Cobalt Strike. What phase in the MITRE ATT&CK framework might this be in will help you provide with additional pivot points when it comes to tactics and techniques. Remember to always think big picture. Where did a particular process come from? Were there any downloads? Who had this file or is communicating with this IP? Lastly, what is the fidelity of this alert? It's advanced because often times, it will be difficult for someone to know the fidelity of an alert without experience. However, if you think about how the event was created, while keeping the pyramid of pain in mind, it can help guide you. 

Here's an example of what you might've foudnd after asking questions:
- Alert triggered because the IP is related to Cobalt Strike
- Condition is satisfied if the IP is related to Cobalt Strike
- Cross referencing the IP with an IP list obtained from a static CTI feed
- Cobalt Strike is a post-exploitation tool commonly used by attackers
- Due to the traffic being inbound with a SYN flag, this could be a sign of reconnaissance
- Low fidelity as IPs are easy to change (think pyramid of pain) and it is based on a CTI feed
  - Although CTI feeds are great, IOCs can change very quickly rendering them useless and outdated

Moving onto, should we be worried? What are the events that must occur to have us worried? You can ask yourself some of these questions:
- Were there an ACK flags sent from the destination IP?
- Using additional OSINT, is this source IP still related to Cobalt Strike?
- Did any other destination IPs get hit with the same source IP?
- Did those IPs send an ACK back to the external IP?
- What were the process creations for this destination host during this time? 

Here are some possible answers to those questions above:
- Check networking logs
  - No ACK flags reported and no other destination IPs were seen
- Performed additional OSINT on source IP
  - Last activity reported back in 2023-05-22, likely not related to Cobalt Struke anymore
- Reviewed process creations for +/- 5 minutes of the alert
  - No suspicious command line arguments or processes that warrant additional investigation
