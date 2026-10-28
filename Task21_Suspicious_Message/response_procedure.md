# Task 21: The Suspicious Message: Decide Before You Act

**Problem Statement:** An employee receives a message threatening account suspension and asking them to confirm details through a link. The message has a company logo but a slightly different sender domain. Decide how to verify it safely and what to do if credentials have already been submitted.

---

## 1. Sample Email (Simulated Phishing Message)

```text
From: IT Support Team <helpdesk@corp-security-verify.com>
To: employee@company.com
Subject: [URGENT] Corporate Account Suspension Notice!

[Company Logo]

Dear Employee,

We noticed unusual login attempts on your work account. To keep your account safe 
and stop it from being suspended within the next 2 hours, please verify your username 
and password right now by clicking the link below:

Link: [hSSp://verify.corp-security-verify.com/login](http://verify.corp-security-verify.com/login)

Thank you,
IT Helpdesk Support
```

---

## 2. Red Flags in the Message (Why It Is Suspicious)

* **Fake Urgency:** The email says the account will be closed soon (within 2 hours). This is done to make the user panic and click without thinking.
* **Wrong Sender Domain:** The sender email is slightly different from the real company domain (`@corp-security-verify.com` instead of `@company.com`).
* **Copied Logo:** Anyone can copy and paste an official company logo into an email. A logo does not prove the email is real.
* **Credential Link:** The message asks the user to click a link to type in their username and password. Real IT teams never ask users to do this via email.

---

## 3. Situation A: What to Do If the User Has NOT Clicked Yet

If the employee only saw the email and did not click the link, follow these safe steps:

1. **Do Not Click or Reply:** Do not click the link, do not download any files, and do not reply to the sender.
2. **Check Link Safely:** Hover the mouse pointer over the link to see the real destination address without opening it.
3. **Verify with IT Separately:** Open a new browser tab and log into the company portal directly. Call or message the IT Helpdesk using the official company phone list or chat (do not use the phone number from the email).
4. **Report the Email:** Report the email so the security team can block the sender address and remove the email from other employees' inboxes.

---

## 4. Situation B: What to Do If Credentials Were Already Submitted

If the user entered their username and password on the fake page, take immediate action in this order:

| Priority / Time | Action Step | Who Does It | Reason / Goal |
| :--- | :--- | :--- | :--- |
| **Step 1**<br>(0 to 5 mins) | Reset Password and End Sessions | User / IT Admin | Change the password immediately and click "Sign out of all sessions" to kick the attacker out of the account. |
| **Step 2**<br>(5 to 15 mins) | Check MFA Settings | IT Admin | Check if the attacker added their own phone number or Authenticator app to keep access. Remove any unknown device. |
| **Step 3**<br>(15 to 30 mins) | Check Login Logs and Email Rules | Security Analyst | Look at recent logins for unknown IP addresses or countries. Check email settings to make sure the attacker did not set up rules to forward or hide emails. |
| **Step 4**<br>(30 to 60 mins) | Scan Device and Block the Link | Security Analyst | Run an antivirus scan on the user's computer. Block the fake website and sender address on the company network so no one else falls for it. |

---

## 5. Decision Table (Action Path)

Use this table to choose the correct steps based on whether the link was opened:

**Trigger:** Suspicious Email Received (Company Logo + Lookalike Domain + Urgent Link)

| Condition 1: User did NOT click the link | Condition 2: User clicked and submitted credentials |
| :--- | :--- |
| 1. Do not click the link or reply to the email.<br>2. Hover the mouse pointer over the link to verify the real URL.<br>3. Contact internal IT Helpdesk using official company chat or phone.<br>4. Report the suspicious email to the security team.<br>5. Security team blocks the sender domain on the gateway. | 1. Reset the account password immediately.<br>2. Terminate all active login sessions across all devices.<br>3. Check MFA configuration and remove any unrecognized device.<br>4. Audit sign-in logs for foreign IP addresses and unusual activity.<br>5. Inspect mailbox rules for hidden or automated forwarding rules.<br>6. Run an antivirus/EDR scan on the user's workstation.<br>7. Block the malicious domain and URL on firewall and email gateway. |

---

## 6. Final Verification Checklist Before Closing Ticket

1. User password has been changed.
2. All active login sessions have been terminated.
3. MFA methods checked and confirmed clean.
4. Email inbox rules checked (no suspicious forwarding rules).
5. Malicious domain and sender blocked on the email filter and firewall.
