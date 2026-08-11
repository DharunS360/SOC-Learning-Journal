## Overview

Today I investigated a phishing alert involving a malicious email attachment in the Let'sDefend SOC environment.

The email contained an attachment that was identified as malicious through threat intelligence analysis. Further endpoint investigation showed that the user opened the file and the system communicated with suspected command-and-control (C2) infrastructure.

I investigated the alert using Email Security, VirusTotal, endpoint telemetry, network activity, and the Case Management Playbook.

![Screenshot 1](../images/1_PDHclrQPKH2Y3zClh9eTAw.png)

## Alert Details

- **Alert:** SOC114 — Malicious Attachment Detected — Phishing Alert
- **Event ID:** 45
- **Event Time:** Jan 31, 2021, 03:48 PM
- **Level:** Security Analyst
- **SMTP Address:** 49.234.43.39
- **Source Address:** accounting@cmail.carleton.ca
- **Destination Address:** richard@letsdefend.io
- **Email Subject:** Invoice
- **Device Action:** Allowed
- **Verdict:** True Positive

## Investigation Process

### 1. Email Security Investigation

I navigated to the **Email Security** tab and searched for the recipient:

`richard@letsdefend.io`

The investigation identified an email sent from:

`accounting@cmail.carleton.ca`

to:

`richard@letsdefend.io`

with the subject:

`Invoice`

The device action was **Allowed**, indicating that the email was permitted by the security control.

**Figure 1 — Email Security Tab**

![Screenshot 2](../images/1_7JQQVLtbEd0zaCMr6_C7zA.webp)

The email contained a suspicious attachment that required further analysis.

**Figure 2 — Email Content**

![Screenshot 3](../images/1_gMPpg1yD7ll9KaW3oknFuA.webp)

### 2. Attachment Analysis

I submitted the suspicious attachment to **VirusTotal** for analysis.

**Figure 3 — VirusTotal Scan Result**

![Screenshot 4](../images/1_NMnHXL6Dn1V_B8uqDryDfA.webp)

VirusTotal identified malicious indicators associated with the submitted file.

I also analyzed the file using its MD5 hash:

`c9ad9506bcccfaa987ff9fc11b91698d`

The hash was also identified as malicious.

**Figure 4 — VirusTotal Hash Analysis**

![Screenshot 5](../images/1_ZlSPPb6OyA3CcXVlM071gg.webp)

The VirusTotal results provided additional evidence that the attachment was malicious.

### 3. File Relationship and Network Indicators

I reviewed the **Relations** section in VirusTotal to identify infrastructure associated with the malicious file.

The analysis revealed contacted domains and IP addresses associated with the file.

**Figure 5 — VirusTotal Relations**

![Screenshot 6](../images/1_u5wl4siLGm99VgIeV9a8JQ.webp)

These indicators were useful for the subsequent endpoint and network investigation.

### 4. Endpoint Security Investigation

I then investigated the affected user's endpoint using the **Endpoint Security** tab.

I searched for the user:

`richard`

to determine whether the suspicious attachment had been opened or executed.

**Figure 6 — Endpoint Security**

![Screenshot 7](../images/1_zSODHEaH4OJJ--SW0-As2g.webp)

The browser history showed a request to:

`http://andaluciabeach.net/image/network.exe`

This indicated that the system had communicated with a suspicious external resource.

**Figure 7 — Browser History**

![Screenshot 8](../images/1_R7xeb62SQLLISKilFbCcJA.webp)

I then reviewed the **Network Action** information and identified communication with:

`5.135.143.133`

This provided additional evidence of communication between the affected system and suspected C2 infrastructure.

**Figure 8 — Network Action**

![Screenshot 9](../images/1_VJZqYTnHxwp6Lo08CkzZgA.webp)

### 5. Host Containment

Since the investigation identified communication with suspected C2 infrastructure, I contained the affected host.

Host containment was performed to prevent further communication with the suspected C2 server and limit potential impact while continuing the investigation.

**Figure 9 — Host Containment**

![Screenshot 10](../images/1_s6EjF2wfoFXIUrC6q5zbdQ.webp)

### 6. Case Management — Playbook Answers

I completed the Case Management Playbook based on the evidence collected during the investigation.

#### Does the Email Contain a Malicious Attachment?

**Yes**

The email contained an attachment that was identified as malicious through threat intelligence analysis.

**Figure 10 — Playbook Answer**

![Screenshot 11](../images/1_0JG50vfbjHasQGiZugFWsw.webp)

#### Is the Attachment Malicious?

**Yes**

The file was identified as malicious based on VirusTotal analysis and the associated MD5 hash.

**Figure 11 — Playbook Answer**

![Screenshot 12](../images/1_f61SemCv-IPvKW_OegGE4Q.webp)

#### Was the Email Delivered to the User?

**Yes**

The device action was **Allowed**, indicating that the email was permitted by the security control.

**Figure 12 — Playbook Answer**

![Screenshot 13](../images/1_faxWp4ncygLIBcZx1s6_Mg.webp)

#### Should the Email Be Deleted?

**Yes**

Since the email contained a confirmed malicious attachment, it should be removed from the recipient's mailbox.

#### Did the User Open the File?

**Yes**

Endpoint evidence showed activity associated with the malicious attachment, including communication with suspicious external infrastructure.

#### Was the Host Contained?

**Yes**

The affected host was contained to prevent further communication with the suspected C2 infrastructure.

## Artifacts

The following indicators were documented during the investigation:

| Type | Indicator |
|---|---|
| Source IP | `49.234.43.39` |
| Source Email | `accounting@cmail.carleton.ca` |
| Destination Email | `richard@letsdefend.io` |
| MD5 | `c9ad9506bcccfaa987ff9fc11b91698d` |
| Suspicious URL | `http://andaluciabeach.net/image/network.exe` |
| Suspected C2 IP | `5.135.143.133` |
| Host User | `richard` |

**Figure 13 — Artifacts**

![Screenshot 14](../images/1_fSTs9I4CMuOLzvL1O4Z6bg.webp)

## Investigation Verdict

**True Positive — Malicious Attachment with Suspected C2 Communication**

The alert was confirmed as a genuine malicious phishing incident.

The email contained a malicious attachment, the email was delivered to the user, and endpoint investigation showed activity associated with the malicious file and communication with suspected C2 infrastructure.

## Response

The affected host was **contained** to prevent further communication with the suspected C2 infrastructure.

The malicious email should be removed from the recipient's mailbox, and the identified indicators were documented as artifacts.

The alert was then closed as a **True Positive**.

**Figure 14 — Closed Alert**

![Screenshot 15](../images/1_ytt7UskSXYK0uuuU1YsUaQ.webp)

## What I Learned

From this investigation, I learned how to:

- Investigate phishing emails containing malicious attachments
- Analyze suspicious files using VirusTotal
- Use file hashes for threat intelligence investigation
- Review file relationships and network indicators
- Investigate endpoint activity
- Identify suspicious external communication
- Understand potential C2 communication
- Perform host containment
- Document investigation artifacts
- Determine True Positive vs False Positive
- Follow a SOC investigation playbook

## Tools Used

- Let'sDefend
- VirusTotal
- Email Security
- Endpoint Security
- Network Action
- Threat Intelligence
- Case Management Playbook

## Key Takeaway

A malicious attachment becomes more significant when endpoint evidence shows that the file was opened and the affected system subsequently communicated with suspicious external infrastructure.

A SOC analyst should correlate:

**Email → Attachment → Hash Analysis → Endpoint Activity → Network Communication → Containment → Playbook → Verdict**

This investigation helped me understand how a SOC analyst can move from detecting a malicious email attachment to identifying potential C2 communication and containing the affected host.
