# Analysis

## Example Alert

**Alert:** Network - Inbound Cobalt Strike IP Detected  
**Time:** 2024-01-10 04:10:10 UTC  
**Source IP:** 40.194.28.30  
**Destination IP:** 172.28.92.7  
**TCP Flag:** SYN

---

## Step 1: Understand the Alert

Begin your analysis by asking the right questions:

- Why did this alert trigger?
- What conditions caused it?
- How was the alert created?
- Why is the system detecting this behavior?
- What phase of the MITRE ATT&CK framework does this align with?
- What is the fidelity of the alert?

These questions guide your thought process and help you define investigation objectives before diving into the logs.

**Example Objective:**  
This alert is triggered by a known Cobalt Strike IP—a tool commonly used by threat actors for post-exploitation. A logical next step is to check for processes making outbound connections to this IP, which may indicate compromise.

Thinking in terms of the MITRE ATT&CK framework also helps guide your analysis toward related tactics and techniques. Always think broadly:  
- Where did the process originate?  
- Was there a download event?  
- Who ran the process?  
- Is this IP seen elsewhere in the environment?

---

## Step 2: Determine Alert Fidelity

Assessing fidelity takes experience, but one way to approximate it is by understanding how the alert was generated.

**Example Breakdown:**

- **Why it triggered:** The IP is tied to known Cobalt Strike infrastructure.
- **Trigger condition:** Match against a static CTI feed.
- **What it means:** Cobalt Strike is often used by attackers after gaining access.
- **Observed behavior:** Inbound SYN traffic suggests possible reconnaissance.
- **Fidelity assessment:** **Low fidelity**  
  - IP-based detections are on the low end of the [Pyramid of Pain](https://detect-respond.blogspot.com/2013/03/the-pyramid-of-pain.html)  
  - IOCs like IP addresses can change frequently and become outdated.

---

## Step 3: Should We Be Worried?

Now that you understand the alert, investigate whether it represents a real threat.

Ask yourself:

- Were any ACK flags sent back from the destination IP?
- Does the source IP still appear malicious based on current OSINT?
- Did this source IP interact with other hosts?
- Did those hosts send any responses?
- What process executions occurred on the destination host around the time of the alert?

**Possible Answers:**

- **Network logs:** No ACKs were seen. No additional destination IPs were contacted.
- **OSINT lookup:** Last known activity for this IP was in May 2023. Possibly outdated.
- **Host logs:** No suspicious process activity around the alert time.

**Conclusion:**  
Should we be worried? **No.**  
Could we be wrong? **Yes—but** our findings are evidence-backed and logically reasoned.

---

## Step 4: Know Your Limitations

Your ability to investigate is limited by available data sources. It's okay to feel overwhelmed, especially if you're new to a SOC role. If you're unsure and need to make a call, ask:

> If I had to decide right now—**is this benign or malicious?**—what would I base that on?

---

## Step 5: Use Prevalence

**Prevalence** is a technique to help you make informed decisions by asking:  
**How common is this artifact in the environment?**

**Example:**  
You find an alert related to `AnyDesk.exe` on a host named `IT-01`.

Ask:
- Do other machines also have `AnyDesk.exe`?
- How many machines executed this file?
- Is this behavior expected on an IT-managed machine?

If **30 out of 30** IT systems have it, you can lean toward **benign**.  
If **1 out of 250** systems has it, that’s **unique**—lean toward **suspicious**.

---

## Caveat: Prevalence Isn’t Perfect

Prevalence should never be your only signal. For example:

- A custom worm could spread across the environment. Its prevalence would be high.
- Yet, the activity would still be **malicious**.
- File hashes might not be flagged by vendors at all.

**Key Takeaway:** Use prevalence **with context.** Combine it with surrounding event data, threat intel, and behavioral patterns to reach a conclusion.

---

> Good analysis isn’t about guessing—it’s about building a case with evidence and asking the right questions to uncover the truth.
