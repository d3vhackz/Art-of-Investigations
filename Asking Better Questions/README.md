# Asking Better Questions

Time is critical in SOC operations. While no questions are inherently bad, some questions are significantly more effective than others. Learning to ask the right questions will help you determine investigation objectives faster, reach conclusions more efficiently, and deliver greater value to your organization.

The key to effective questioning lies in building a logical framework that moves you from uncertainty to evidence-based conclusions.

---

## The Question Framework

Start with the fundamental question and work your way down through increasingly specific layers:

### Level 1: Core Assessment
**Is this a false positive or true positive?**

### Level 2: Scenario Analysis
**What are the possible scenarios that would make this a false positive or true positive?**

### Level 3: Hypothesis Testing
**What specific questions can I ask to prove or disprove each scenario?**

### Level 4: Evidence Gathering
**Where can I look to find answers (be as specific as possible)?**

---

## Question Quality Standards

Effective investigation questions should be:

- **Relevant** to the specific event or alert
- **Specific** enough to generate actionable answers
- **Answerable** with available data sources and tools

Avoid vague questions like "Is this bad?" Instead, ask targeted questions that lead to concrete evidence.

---

## Practical Example: PsExec Usage Alert

**Alert Details:**
- **Alert:** PsExec Usage Identified
- **Time:** 2024-01-03 19:10:20
- **User:** admin_john
- **Host:** SRV01
- **Process:** PsExec.exe

### Applying the Framework

**Level 1: Core Assessment**  
Is this PsExec usage a false positive or true positive?

**Level 2: False Positive Scenarios**
- Scheduled maintenance on SRV01
- PsExec is an authorized tool previously used by this account
- John is conducting legitimate testing activities

**Level 3: Questions to Test False Positive**
- Is there scheduled maintenance on SRV01 right now?
- Has admin_john used PsExec before in this environment?
- Is John currently working and aware of this activity?

**Level 4: Evidence Sources for False Positive**
- **Ticketing System:** Search for maintenance tickets on SRV01
- **SIEM Historical Search:** Query 7-30 days for PsExec usage by admin_john
- **User Verification:** Check John's status on Teams and confirm activity directly

**False Positive Investigation Results:**
- ✅ **Ticketing System:** Found maintenance ticket for SRV01 scheduled 2024-01-03 19:00-20:00
- ✅ **SIEM Search:** Historical PsExec usage by admin_john confirmed
- ✅ **User Confirmation:** John confirmed ongoing maintenance via Teams

**Conclusion:** False positive - legitimate maintenance activity

---

**Level 2: True Positive Scenarios**
- PsExec is an unauthorized application in this environment
- John's account is compromised while he's unavailable
- No legitimate business reason for this activity

**Level 3: Questions to Test True Positive**
- Is this the first occurrence of PsExec in the environment?
- Where and how did admin_john authenticate for this session?
- Is John currently available and working?
- Is there any scheduled maintenance for SRV01?

**Level 4: Evidence Sources for True Positive**
- **SIEM Historical Search:** Query environment-wide for any PsExec usage
- **Authentication Logs:** Check Event ID 4624 for admin_john login details
- **User Status:** Verify John's availability through Teams and Exchange
- **Ticketing System:** Confirm no scheduled maintenance

**True Positive Investigation Results:**
- 🚨 **SIEM Search:** First PsExec occurrence; command line contains suspicious random executable
- 🚨 **Authentication Logs:** Logon Type 10 (RDP) from China (company based in US)
- 🚨 **User Status:** John is out of office 2024-01-01 to 2024-01-07
- 🚨 **Ticketing System:** No maintenance tickets found

**Conclusion:** True positive - likely account compromise

---

## Key Takeaways

1. **Start broad, get specific** - Move from general assessment to targeted evidence gathering
2. **Consider multiple scenarios** - Don't tunnel vision on the first explanation that comes to mind
3. **Know your data sources** - Understand exactly where to look for each type of evidence
4. **Document your reasoning** - Clear questions lead to clear investigation narratives
5. **Time-box your questioning** - Don't get stuck in analysis paralysis

---

> The quality of your investigation is directly tied to the quality of your questions. Ask better questions, get better answers.
