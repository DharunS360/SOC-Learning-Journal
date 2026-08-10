# Day 03 — SOC140: Phishing Mail Detected — Suspicious Task Scheduler

![screenshot 1](../images/1_PDHclrQPKH2Y3zClh9eTAw.png)

## Detection Summary

**Event ID:** 82

**Event Time:** Mar 21, 2021, 12:26 PM

**Rule:** SOC140 — Phishing Mail Detected — Suspicious Task Scheduler

**Level:** Security Analyst

**SMTP Address:** 189.162.189.159

**Source Address:** aaronluo@cmail.carleton.ca

**Destination Address:** mark@letsdefend.io

**Email Subject:** COVID19 Vaccine

**Device Action:** Blocked


## Investigation Process

### 1. Email Security Investigation

I started the investigation by navigating to the **Email Security** tab and searching for the sender:

`aaronluo@cmail.carleton.ca`

This allowed me to identify the suspicious email associated with the alert.

**Figure 1 — Email Security Tab**

![screenshot 2](../1_6NGk2IdbdKzx94n6PJkbyQ.webp)

The email with the subject **"COVID19 Vaccine"** showed several phishing indicators.

The message used a COVID-19-related subject and an urgent call to action, encouraging the recipient to open the attached file immediately. The use of a randomly named ZIP file as an attachment was another suspicious indicator.

**Figure 2 — Suspicious Email**

![screenshot 3](../1_4AwAdBqHqiO_DI03ogMZqA.webp)


### 2. File Analysis

The suspicious attachment was downloaded and analyzed in an isolated lab environment.

> **Note:** Suspicious or potentially malicious files should be analyzed only in an isolated environment such as a virtual machine.

I first submitted the file to **VirusTotal** for analysis.

### VirusTotal Results

VirusTotal showed that **31 security vendors and 1 sandbox** flagged the file as malicious. Several vendors classified the file as a **Trojan**.

**Figure 3 — VirusTotal Scan Result**

![screenshot 4](../1_2MafrIticL4SfbWLMGFBXw.webp)

I then submitted the same file to **Hybrid Analysis** for additional sandbox analysis.

### Hybrid Analysis Results

The file with the hash:

`72c812cf21909a48eb9cceb9e04b865d`

was also identified as malicious by Hybrid Analysis.

The results from both VirusTotal and Hybrid Analysis provided additional evidence that the attachment was malicious.

**Figure 4 — Hybrid Analysis Results**

![screenshot 5](../1_18hp7bC8pnD6h9RowjOEvQ.webp)

### 3. Email Delivery Investigation

Although the sender and intended recipient were known, I needed to determine whether the email reached the mail infrastructure.

I navigated to **Log Management** and searched using the SMTP/source IP:

`189.162.189.159`

The investigation showed the following destination information:

- **Destination IP:** `172.16.20.3`
- **Port:** `25`

**Figure 5 — Log Management**

![screenshot 6](../1_BBd3H2o-wXJ87HK5aQ1csw.webp)

### 4. Endpoint Security Investigation

Next, I used the destination IP identified during the log investigation to investigate the associated endpoint.

The endpoint information showed that the destination was the **MS Exchange Server**.

I then reviewed the process history and terminal/command history to determine whether any suspicious activity occurred on the system.

**Figure 6 — Endpoint Security**

![screenshot 7](../1_pt7rhTJ_AtHgPcCXeuuEeQ.webp)

**Figure 7 — Event ID**

![screenshot 8](../1_JIjbUZYMzSZiajWFfA4bIw.webp)

**Figure 8 — Terminal History**

![screenshot 9](../1_T2NhYRQul33t8XARbpiWTA.webp)

The investigation did not reveal any suspicious activity. This was consistent with the fact that the email had already been **blocked**.

## Artifacts

The relevant indicators identified during the investigation were documented as artifacts.

**Figure 9 — Artifacts**

![screenshot 10](../1_POo35k38yaVnnnne3Hkndg.webp)

## Case Management — Playbook Answers

### 1. Are There Any Attachments or URLs?

**Yes**

The email contained a suspicious file attachment.

### 2. Is the Attachment Malicious?

**Yes**

The attachment was identified as malicious by both **VirusTotal** and **Hybrid Analysis**.

### 3. Was the Mail Delivered to the User?

**No**

The email was blocked by the security controls and was not delivered to the intended user.

### 4. Was the Alert a True Positive?

**Yes**

The alert was confirmed as a **True Positive** because the email contained a malicious attachment and the security controls successfully blocked it.

**Figure 10 — Playbook**

![screenshot 11](../1_wI1O2xLxsdWg9NqftFKezw.webp)

## Investigation Verdict

**True Positive — Phishing Email with Malicious Attachment**

The investigation confirmed that the alert was a genuine phishing-related incident.

The malicious attachment was detected by multiple security vendors and sandbox analysis tools. The email was also blocked, preventing it from being delivered to the intended user.


## Response

The email was **blocked**, preventing the suspicious attachment from reaching the intended recipient.

No additional suspicious activity was identified during the endpoint investigation.

The relevant indicators were documented as artifacts, and the alert was closed as a **True Positive**.

**Figure 11 — Closed Alert**

![screenshot 12](../1_044KsNV8Fa3Ne4Pcdv9mEA.webp)

## What I Learned

From this investigation, I learned how to:

- Investigate phishing email alerts
- Identify suspicious email characteristics
- Analyze malicious attachments
- Use VirusTotal for malware analysis
- Use Hybrid Analysis for sandbox analysis
- Investigate email delivery using logs
- Review endpoint activity
- Determine whether an email was delivered
- Document security artifacts
- Determine True Positive vs False Positive
- Follow a SOC investigation playbook


## Tools Used

- Let'sDefend
- VirusTotal
- Hybrid Analysis
- Email Security
- Log Management
- Endpoint Security
- Case Management Playbook


## Key Takeaway

A phishing email should not be judged only by its subject or sender. A SOC analyst should correlate multiple sources of evidence such as:

**Email Analysis → Attachment Analysis → Threat Intelligence → Log Investigation → Endpoint Investigation → Playbook → Verdict**

In this investigation, the malicious attachment was identified by multiple security analysis tools, while the email was blocked before it could be delivered to the intended user.

This investigation helped me understand how a SOC analyst investigates phishing emails and validates alerts using multiple sources of evidence.
