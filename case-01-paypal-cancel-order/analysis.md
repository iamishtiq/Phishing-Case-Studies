# Case 01 – PayPal "Cancel Order" Phishing Email Analysis

## Overview

In this case, I analyzed a suspicious email pretending to be from PayPal regarding a cancelled order. The email attempts to create urgency and manipulate the recipient into clicking a malicious link.

The objective of this analysis is to identify phishing indicators, extract IOCs, and understand the attacker’s techniques.

---

## 1️⃣ Email Header Analysis

![Email Header Analysis](screenshots/01-image-header.png)

### Observations:

- The sender email address appears suspicious and does not match PayPal's official domain.
- The display name tries to impersonate PayPal.
- The domain does not belong to `paypal.com`.
- This is a common phishing tactic: spoofing trusted brands.

### Red Flag:
Mismatch between sender name and actual sender email address.

---

## 2️⃣ Email Body Analysis (Part 1)

![Email Body Part 1](screenshots/02-email-body-1.png)

### Observations:

- The email claims that an order was cancelled.
- It creates urgency by implying account activity.
- It encourages the victim to take immediate action.

### Psychological Technique Used:
**Urgency + Fear**

The attacker wants the victim to panic and click without verifying.

---

## 3️⃣ Email Body Analysis (Part 2)

![Email Body Part 2](screenshots/03-email-body-2b.png)

### Observations:

- The email includes a "Cancel the order" button.
- The language pressures the victim to act quickly.
- No proper personalization (generic greeting).

### Red Flags:
- Generic message
- Suspicious action button
- Emotional manipulation

---

## 4️⃣ Suspicious Action Button (HTML Inspection)

![Cancel Order Button](screenshots/04-cancel-order.png)

To verify where the **"Cancel the order"** button actually redirects, I inspected the raw HTML of the email.

### Extracted HTML Code

```html
<a type="Link" isLinkToBeTracked="true" target="_blank"
href="https://is.gd/6OCJ4m#-u7g;ah7Je1">
Cancel the order
</a>
```


---

## 5️⃣ URL Shortener Investigation

![URL Shortener](screenshots/05-email1-url-shortener.png)

After identifying that the "Cancel the order" button used a shortened URL (`https://is.gd/6OCJ4m`), I expanded the link using an online URL expander tool to reveal its final destination.

### Result of URL Expansion

The shortened link redirected to:

- https://www.google.com

The screenshot above shows the expanded result, displaying a Google landing page (in German language settings).

### Analysis

At first glance, redirecting to Google may seem harmless. However, this behavior is still suspicious for several reasons:

- PayPal would never use a URL shortening service.
- PayPal would never redirect users to Google for transaction cancellation.
- Attackers often:
  - Test phishing campaigns using safe redirects.
  - Use temporary redirects before switching to malicious pages.
  - Avoid detection by pointing links to legitimate websites during analysis.

### Why This Still Indicates Phishing

Even though the final destination is Google:

- The sender email is spoofed.
- The recipient address is unusual.
- The link is obfuscated using a shortening service.
- The email creates urgency about a $120 payment.

This confirms the email is malicious regardless of the redirect behavior.






---

## Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| Sender Email | noreplyexmhwje9hhzdgInve9ml1xqzypnedg51ny7yleqejbwe@sultanbogor.com |
| Display Name | service@paypal.com |
| Shortened URL | https://is.gd/6OCJ4m |
| Transaction ID | 74221905U |
| Impersonated Brand | PayPal |


---

## MITRE ATT&CK Mapping

- **T1566.002 – Phishing: Spearphishing Link**
- **T1204 – User Execution**
- **T1036 – Masquerading**

---

## Risk Assessment

Severity: Medium  
Confidence Level: High  

Reason:
Brand impersonation + shortened link + urgency-based manipulation.


### Security Lesson

Never trust shortened URLs in financial transaction emails.  
Always verify the domain before interacting with any link.

If unsure:
- Manually type the official website (e.g., paypal.com) in your browser.
- Check transactions directly inside your account dashboard.

---

## Conclusion

This case demonstrates how simple but effective phishing techniques still rely heavily on human psychology rather than technical exploitation.

Understanding these indicators helps improve detection and response in a SOC environment.

---

**Author:** Ishtiaq Rashid  
Cybersecurity Analyst (Aspiring SOC Analyst)

