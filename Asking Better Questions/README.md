# Asking Better Questions

Although no questions are bad questions, there are questions that are better than others. And as a SOC analyst, where time is of the essence, it is a good idea ot know how to start asking the right questions to make your investigations efficient and valuable. It will help you determine your objectives and conclude your investigations quicker. 

So how do you ask the right questions?

- Is this a false positive or true positive? (What are some possible scenarios that makes this a false positive?)
  - What are the conditions for this to be a false positive or a true positive?
    - What questions can I ask to prove or disprove this?
      - Where can I look to find my answer (as specific as possible)?
     
Questions should be:
- Relevant to the event
- Specific to the event
- Answerable to the event

Example alert:
Alert: PsExec Usage Identified
Time: 2024-01-03 19:10:20
User: admin_john
Host: SRV01
Process: PsExec.exe

Is this a false positive or true positive?
- What are some possible scenarios that  makes this a false positive?
  - Scheduled maintenance on SRV01
  - PsExec is marked as an authorized tool and used in the past from this account
  - John is testing with PsExec
    - Unless it's an insider threat
- What questions can I ask to prove or disprove this?
  - Is there a maintenance happening on SRV01 right now?
  - Has admin_john ever ran PsExec before?
  - Is John working right now?
- Where can I look to find answers (as specific as possible)?
  - View ticketing system and look for scheduled maintenance
    - Found a ticket stating maintenance will occur on SRV01 between 2024-01-03 19:00 to 20:00
  - Run a search across 7-30 days on the SIEM for processes containing PsExec from admin_john
    - Observed previous usage of PsExec
  - Check John's status on messaging app such as Teams and ping John for confirmation
    - John confirmed on-going maintenance

- What makes this a true positive?
  - PsExec is an unauthorized application
  - John is on vacation and someone is using his account
  - There is no scheduled maintenance for SRV01
- What question can I ask to prove or disprove this?
  - Is this the first time seeing PsExec in the environment?
  - Where did admin_john login from and how?
  - Is John working right now?
  - Is there a scheduled maintenance for SRV01?
- Where can I look to find my answer (as specific as possible)?
  - View ticketing system and look for scheduled maintenance
    - No ticket opened
  - Run a search across 7-30 days on the SIEM for processes containing PsExec
    - First occurence and only account using it and command line contains a random executable name
  - Check Windows Security Event ID 4624 (Account Logon Successful) event for admin_john
    - Found Logon Type 10 (Remote Desktop) where the source is from China (company is based in the US)
  - Check John's status on Teams & Exchange
    - John is out of office from 2024-01-01 to 2024-01-07
