# 🔍 Investigation Questions
## Operation: Cipherlock — Forensics Analysis

Answer each question in a new file: `forensics/my_answers.md`  
Use evidence from `server_log.txt`, `email_header.txt`, and `file_metadata.txt` to support every answer.

---

### Section A — Server Log Analysis

**Q1.** What is the username of the primary suspect? What evidence from the server log supports this? 
jdoe92, Evidence that supports this is that he used admin controls to access confidential information.

**Q2.** At what time did the suspect's activity become suspicious? What specifically changed between their daytime and nighttime sessions? (Look at IP addresses AND files accessed.)
[2026-04-18 23:47:38] This is the time at which the suspect's activity became suspicious. Specifically between daytime and nighttime seesions, the suspect's IP address changed from 192.168.1.102 to 10.45.88.201, and the types of files they were accessing also differed.

**Q3.** List every file the suspect downloaded during the suspicious session. Why would each of these files be considered sensitive or confidential?
[2026-04-18 23:47:02] jdoe92 10.45.88.201 GET /clients/records/ 200
[2026-04-18 23:47:38] jdoe92 10.45.88.201 GET /clients/records/ALL_CLIENT_DATA.zip 200
[2026-04-18 23:48:15] jdoe92 10.45.88.201 GET /clients/records/FINANCIAL_MASTER.xlsx 200
[2026-04-18 23:49:01] jdoe92 10.45.88.201 GET /clients/records/SSN_DATABASE.csv 200
[2026-04-18 23:51:44] jdoe92 10.45.88.201 POST /admin/export.php 200
[2026-04-18 23:52:30] jdoe92 10.45.88.201 GET /logout 200

Each of these files would be considered confidential because it's all sensitive employee info ranging from personal info to financial info, and as well was extracted using admin commands.

**Q4.** One of the entries in the server log shows a POST request to `/admin/export.php`. What does a POST request mean, and why is this action more concerning than a GET request in this context?
A POST request would just clarify the type of way data is being sent, which in this case is concerning compared to a GET request because rather than just collecting data from the URL, the POST request is doing it in the body of the HTTP request, meaning it's not visible in the URL. This action immediatly raises cause for suspicion/investigation.

---

### Section B — Email Header Analysis

**Q5.** What is the originating IP address of the email? How does this connect to the server log?
The originating IP is 209.85.214.201


**Q6.** Why is the use of ProtonMail significant in this investigation? What does it suggest about the suspect's intent?
It's significant because ProtonMail is a encryption based company. This suggests possible malicious intent. 

**Q7.** The email subject line is blank. Why might a suspect deliberately send an email with no subject? What technique might they be using?
They might do this to avoid spam filters so that they can implement reconnaissance techniques. 

**Q8.** Compare the email timestamp to the server log. What does the timeline suggest about the order of events on the night of April 18?
It suggests that the suspect deliberately sent those blank emails before accessing and extracting sensitive info for malicious intents.
---

### Section C — File Metadata Analysis

**Q9.** The three large data files (`.zip`, `.xlsx`, `.csv`) all have the same "Created" date and time range. What does this tell you about how they got onto the USB drive?
This suggests that they were most likely physically probed onto the USB by the suspect.

**Q10.** The "Last Accessed" timestamp on every file is `2026-04-19 08:15:01`. Why are they all identical? What event caused this?
They're all identical because they were all opended at the same time.

**Q11.** `note_to_self.txt` was created at `23:44:00` and the email was sent at `23:32:00`. Does this timeline make sense given what the note contains? Explain.
The timeline makes sense because of what the suspect had implemented onto the note, as well as what the email contains.
---

### Section D — Putting It All Together

**Q12.** Write a 1–2 paragraph **incident summary** describing what you believe happened on the night of April 18, 2026. Use specific evidence (timestamps, filenames, IP addresses) to support your conclusion. This is similar to what a real digital forensics analyst would write in an official report.
Based on my investigation, on the night of April 18, 2026, someone on the inside of the company deliberately stole employee information from the servers' backup files. This info includes personal, financial, and company files that were uploaded to an encypted USB drive and sold off to a malicious user. Their plan to accomplish this does not contain a specific start date based off of the given info, however, there was evidence of blank encrypted emails sent using ProtonMail, a service know for anonymity. This evidence is reasoning as to what led to the situation which had occured that night.

**Q13.** What laws or regulations might the suspect have violated? Name at least TWO (examples: CFAA — Computer Fraud and Abuse Act, HIPAA, FERPA, state data breach laws).
Laws/regulations that they may have violated include the Defend Trade Secrets Act (DTSA), the Economic Espionage Act (EEA), and state-level laws such as the Uniform Trade Secrets Act (UTSA).

**Q14.** If you were the IT security team, what THREE security measures could have prevented or detected this breach earlier?
Three things they could do better would be to implement better UAC, create a software that filters suspicious emails more efficiently and accurately, and lastly, to have stronger backup servers.
