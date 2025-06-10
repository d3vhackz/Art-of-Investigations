# Triage

Triage is the process of rapidly assessing incoming alerts to determine their urgency and prioritize response. It’s one of the core responsibilities of a SOC analyst. The faster and more accurately you can triage, the faster you can either escalate a real threat or move on from false positives—maximizing efficiency and minimizing risk.

## Objectives of Triage

There are two main goals when triaging alerts:

1. **Determine Priority**  
   Identify which alerts should be addressed first based on severity, fidelity, and potential impact.

2. **Assess Relevance**  
   Decide whether an alert represents legitimate malicious activity or a false positive.

## Key Questions to Ask During Triage

To guide your triage process, ask yourself the following:

1. **What is the severity of the alert?**  
   - Higher severity typically means higher urgency.  
   - Many SOCs rank severity from 1 (critical) to 5 (informational).

2. **Are multiple alerts of the same type triggering?**  
   - Group similar alerts to reduce noise and recognize patterns.  
   - Repeated alerts could indicate a persistent issue or attack campaign.

3. **Are there any high-fidelity alerts?**  
   - High-fidelity alerts rarely trigger but are highly reliable.  
   - These alerts often indicate confirmed malicious behavior and should be prioritized.

4. **How was the alert generated?**  
   - Was it triggered by a signature-based detection?  
   - Is it a custom detection built by your threat detection team?  
   - Is the alert correlated across multiple sources?

## Example Scenario

You're working an overnight shift at an MSSP. Suddenly, 50 alerts are generated within a few minutes—each with different severities and sources. Your task is to determine which alerts deserve immediate attention.

Ask yourself:

- Are there any **Severity 1** alerts?
- How many alerts are **duplicates or related**?
- Are any of these **custom alerts** built by detection engineers?
- Which alerts, if ignored, could result in significant damage?

By working through these questions, you can quickly separate signal from noise and focus your time and effort where it matters most.

---

> Triage isn’t about investigating everything—it's about knowing **what to investigate first and why.**
