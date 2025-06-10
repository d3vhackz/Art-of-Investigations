# Triage

An assessment to determine the urgency of an event. It's one of the main responsiblities of a SOC analyst. The quicker you can triage, the quicker you can move onto another alert or respond to an active incident. The objective for triaging is to identify which alert should be treated with the highest priority. In other words, which one should you focus on first? The second objective is to determine if the received alert is something you should be worried about. 

To help with triage, you can ask yourself a couple of questions. 
1. What are the severities of these alerts? (Typically, the higher the severity, the higher the priority. And lower the severity, the lower the priority)
2. How many of the same alert is triggering? (You want to group alerts as much as possible to clean things up and improve prioritization)
3. Are there any high fidelity alerts? (High fidelity alerts are alerts that rarely trigger, and if they do trigger it is almost certain that malicious activity is happening)
4. How did this alert generate?

Example:
You're working in an overnight shift at an MSSP as a SOC analyst. 50 alerts come in within minutes, each with different severities. You need to identify which alerts should be triaged with the highest priority and determine if this alert is something you should be worried about. Some good questions you can ask are:
1. Are there any severity 1 (1 being the highest) alerts?
2. Out of the 50 alerts, which ones are the same?
3. Which alerts are custom alerts?
4. Are there any alerts that are more "dangerous" than others if neglected?
