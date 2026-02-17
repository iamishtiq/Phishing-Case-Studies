# Case 01: PayPal Order Cancellation Phishing Email

## 1. Overview

This case involves a phishing email impersonating PayPal. The attacker attempts to trick the recipient into believing an unauthorized transaction has occurred and urges them to cancel the order immediately.

The email uses brand impersonation and URL shortening services to hide the final redirection destination.

---

## 2. Initial Observations

- Subject: "Cancel your PayPal order"
- Displayed Sender Name: service@paypal.com
- Actual Sender Email: gibberish@sultanbogor.com
- No attachments included
- One interactive element: "Cancel the order" button

---

## 3. Red Flags Identified

### 3.1 Sender Email Mismatch

The displayed sender name suggests the email is from PayPal.  
However, the actual sender domain is:

sultanbogor.com

This mismatch is a strong indicator of spoofing.

---

### 3.2 Suspicious Recipient Address

The email was not sent to the legitimate Yahoo account address.  
This discrepancy suggests mass phishing distribution or spoofed targeting.

---

### 3.3 Social Engineering Technique

The subject line creates urgency by implying:

- A recent purchase
- Possible financial loss
- Immediate action required

This is a classic psychological trigger to bypass rational thinking.

---

## 4. Technical Analysis

### 4.1 HTML Brand Impersonation

The email body was carefully formatted using HTML to resemble a legitimate PayPal notification.  
Logos, formatting, and layout were used to increase credibility.

---

### 4.2 URL Shortening Abuse

The "Cancel the order" button used a shortened URL instead of a direct PayPal link.

Shortened URLs hide the real destination and prevent users from identifying malicious domains by hovering over links.

Using an online URL expansion tool revealed:

- The shortened URL redirected to google.com

Although this sample redirects to a benign site, attackers often use this method to redirect victims to:
- Credential harvesting pages
- Malware delivery sites
- Payment fraud portals

---

## 5. MITRE ATT&CK Mapping

- T1566.002 – Phishing: Link
- T1036 – Masquerading
- T1204 – User Execution

---

## 6. Indicators of Compromise (IOCs)

- Sender domain: sultanbogor.com
- Spoofed display name: service@paypal.com
- Use of URL shortening service
- Phishing-style financial urgency message

---

## 7. Risk Assessment

Medium to High Risk

Although this specific sample redirected to google.com, the techniques used are consistent with real-world financial phishing campaigns.

If weaponized, this attack could result in:

- Credential theft
- Financial fraud
- Account takeover

---

## 8. Recommended SOC Actions

- Block sender domain at the email gateway
- Flag similar spoofed PayPal patterns
- Alert users about PayPal impersonation campaigns
- Implement URL detonation/sandbox analysis for shortened links
- Enable DMARC, DKIM, and SPF enforcement

---

## 9. Lessons Learned

This case demonstrates how:

- Brand impersonation increases trust
- Urgency triggers emotional reactions
- URL shorteners obscure malicious intent
- Header analysis is critical in phishing investigations

This investigation highlights the importance of verifying sender domains and inspecting embedded hyperlinks before interacting with suspicious emails.

