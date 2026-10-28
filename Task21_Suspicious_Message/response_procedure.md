# Task 21: The Suspicious Message: Decide Before You Act

## Scenario
An employee of a fictional company, AcmeCorp (official domain: acmecorp.com), receives a message that threatens account suspension within 24 hours and asks them to confirm details through a link. The message has the company logo, but the sender domain is slightly different (for example acmec0rp.com, with a zero instead of the letter o).

This document gives a response procedure for two situations:
- **Situation A:** the employee has not clicked or entered anything.
- **Situation B:** the employee has already submitted credentials.

## Assumptions
- The company uses single sign-on with MFA.
- A security or IT contact exists, and there is a way to report phishing (button or mailbox).
- The employee is not a security specialist.
- The first priority is limiting harm quickly; the second is learning from the event.

## Evidence assessment
| Clue | What it suggests | Weight |
|---|---|---|
| Sender domain differs slightly from the real one | Lookalike domain, a common phishing technique | Strong |
| Link may point to a different domain than it displays | Deceptive link (must be checked without clicking) | Strong, needs verification |
| Asks to confirm details through a link | Genuine IT teams rarely ask for credentials via emailed links | Strong |
| Threat and 24-hour deadline | Urgency is used to stop careful thinking; real notices can also be urgent | Medium |
| Generic greeting, unexpected message | Typical of mass phishing, weak on its own | Weak |
| Company logo present | Easy to copy, gives no assurance | Negligible |

**Judgement:** two strong indicators (lookalike domain and a credential request through a link) plus urgency make phishing the working conclusion. The message should still be verified through an independent channel, and passing every check would not prove it is genuine.

## Situation A: nothing clicked or entered

### Decision procedure
1. **Stop.** Do not click, reply, open attachments, call numbers in the message, or forward it to colleagues.
2. **Inspect without interacting.**
   - Read the full sender address, not just the display name.
   - Check the Reply-To address.
   - Look at SPF, DKIM and DMARC results in the message headers.
   - Hover (desktop) or long-press (mobile) the link to read the real URL.
3. **Question: do the sender and link domains exactly match the official domain?**
   - **No:** treat as phishing. Go to step 6.
   - **Yes or unsure:** go to step 4.
4. **Verify independently.** Open the service by typing the official address or using a bookmark or app. Look for a matching notice. Or ask IT through a known contact. Never use anything from the message itself.
5. **Question: does the independent channel confirm the message is genuine?**
   - **Yes:** it is legitimate. Act only through the official site, never through the link.
   - **No or unsure:** treat as phishing. Go to step 6.
6. **Report.** Use the Report Phishing button or forward the message to the security mailbox.
7. **Delete after reporting.**
8. **Security team follow-up:** search all mailboxes for the same sender or subject, remove matches, block the domain and URL, check proxy logs for anyone who clicked, and warn staff.

### Do and do not
| Step | Do | Do not |
|---|---|---|
| Pause | Treat the message as unverified | Click, reply, or call numbers in it |
| Inspect | Check the full address, headers and real URL | Trust the display name or the logo |
| Verify | Use the official site or a known contact | Use any link or contact from the message |
| Report | Report first, then delete | Delete without reporting |

## Situation B: credentials already submitted

**Principle:** the attacker moves faster than we do, so contain first, investigate second. A fake page can also steal the session, so changing the password alone is not enough.

### Response procedure
1. **Minutes 0 to 5: tell IT/Security immediately** by phone or chat. Do not wait to be sure, and do not delete the message (it is evidence).
2. **Minutes 0 to 10: the employee secures the account.** From a clean device, open the official site by typing its address, change the password, and sign out of all sessions. Change any other account that uses the same password.
3. **Security team contains the account:**
   - force a password reset
   - revoke sessions and refresh tokens
   - review and reset MFA methods, removing unknown devices
   - block the sender domain and URL
   - remove the message from all mailboxes
4. **Security team scopes the damage:** check sign-in logs (new IP, location or device), mailbox rules and forwarding, OAuth app consents, sent mail, file downloads and privileged actions.
5. **Question: is there evidence of attacker activity, or was other data entered (ID, payment details, an MFA code)?**
   - **Yes:** declare an incident. Isolate the device if malware is suspected, reset all affected accounts, escalate to data-protection or legal, and notify affected parties where required.
   - **No:** monitor the account for 30 days, require re-verification, and record the outcome.
6. **Post-incident:** preserve evidence, hold a blame-free debrief, send an awareness reminder, and improve detection.

**If the employee only clicked and entered nothing:** report it, scan the device, change the password as a precaution, and monitor.

### Who does what
| Role | Responsibilities |
|---|---|
| Employee | Report immediately, change the password from a clean device, sign out everywhere, say what was entered and on which device |
| IT / Security | Force reset, revoke sessions, review MFA methods and mailbox rules, check logs, block domain, remove message, isolate device if needed |
| Manager / HR / Legal | Support the employee without blame, involve data-protection or legal if personal data was exposed |

### Why these checks
- **Session and token revocation** removes an attacker who is already logged in, which a password change alone does not.
- **Mailbox rules and MFA methods** are common persistence tricks, because attackers hide replies or add their own device.
- **Sent mail** shows whether the account is being used to phish colleagues.
- **If an MFA code was typed in**, assume the attacker may have a live session until logs show otherwise.

## Common mistakes avoided
- Clicking "unsubscribe" or replying to check if it is real.
- Calling the phone number in the message.
- Changing the password on a possibly infected device, or changing it without ending active sessions.
- Deleting the message before reporting it.
- Waiting to see if anything happens after submitting credentials.

## Prevention and measurement
- DMARC at enforcement and external-sender banners.
- Monitoring and blocking lookalike domains.
- Phishing-resistant MFA such as passkeys.
- A one-click Report Phishing button and a blame-free culture.
- **Metrics:** time to report, report rate in phishing simulations, click rate, and time from report to message removal.

## Limitations
This is a general procedure for a fictional organisation. Real steps depend on the mail platform, identity provider and legal duties such as breach-notification deadlines. The clue weights are judgement-based, not a formal scoring standard.

## References
- NIST SP 800-61 Rev. 3, Incident Response Recommendations and Considerations for Cybersecurity Risk Management
- NIST SP 800-63B, Digital Identity Guidelines
- CISA, FBI, NSA and MS-ISAC, Phishing Guidance: Stopping the Attack Cycle at Phase One (2023)
- MITRE ATT&CK T1566 (Phishing)
