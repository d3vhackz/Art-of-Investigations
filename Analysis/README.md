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

Conclusion: Should we be worried? No. Is it possible to be wrong? Yes, but because of the questions we asked and investigation we did, we have proof or evidence that supports the opposite. 

Do keep in mind that your investigation is heavily impacted depending on the data sources that are available to you. 

If you are brand new to the SOC and just starting out, it is very easy to get lost in all the alerts and events that are happening and each alert that you attempt to triage and perform analysis on. You might not know what to do, and that's perfectly okay. If your back was against the wall and you had to make a decision on if an alert was benign or malicious, how would you make that decision? 

One common method I like to use is called prevalence, and it may not apply everywhere but it is something for you to try and fall back on when doing your analysis. Prevalence is use to determine how common something is. For example, imagine you are investigating an alert that had AnyDesk on a machine named IT-01. Your objective should be to determine if we should be worried or not, aka is this benign activity or malicious activity. 

Some of the questions you can ask are how common is the file AnyDesk.exe? Do other hosts have this file? Did any of them execute this file? For example if you identified that all 30 IT computers have AnyDesk, the prevalence would be common and you can lean towards it being benign. But if only 1 of 250 computer have AnyDesk, the prevalence is unique and you can lean towards it being malicious. 

As a side note, there are multiple different conclusions in every SOC environment, but for the sake of this example, we only have two outcomes, which benign or malicious. And as a unique example, if an adversary deployed a custom worm to your environment, you won't find any security vendors flagging the file hash as malicious and worms spread themselves, so many computers would have it, making the prevalence common. This is why you shouldn't solely rely on prevalence but use it as a method, along with researching surrounding events and looking at the bigger picture to help you draw your conclusion.
