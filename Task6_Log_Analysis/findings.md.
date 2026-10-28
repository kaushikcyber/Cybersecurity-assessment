# Task 6: Decode and Interpret Security Logs

## Objective
Analyse a small synthetic authentication log, describe normal behaviour, and identify which observations need further investigation.

## Dataset
sample_auth.log: 24 synthetic events, 3 regular users (anna, ravi, meera), 27 to 28 October 2026. Totals: 16 LOGIN_SUCCESS, 8 LOGIN_FAILURE.

## Normal behaviour
- Each regular user logs in from one internal IP: anna 10.0.0.5, ravi 10.0.0.6, meera 10.0.0.7.
- Normal logins fall between about 08:55 and 16:50.
- Failures from internal IPs are rare: 2 of 18 internal events.

## Findings

**F1: Many failures from one external IP, then a success (High)**
- Evidence: 198.51.100.23 failed 6 times in 30 seconds (11:00:00 to 11:00:30) against 6 different usernames (admin, root, test, anna, ravi, meera), then succeeded as ravi at 11:00:36.
- Why unusual: one outside source trying many accounts at a steady 6-second rhythm looks automated, and ravi has never used this IP.
- Harmless explanation: ravi on a new network (unlikely, given the failures against other users).
- Next steps: reset ravi's credentials, review his session from 11:00:36, block the IP, check other logs for the same source.

**F2: Login at 03:14 (Low to Medium)**
- Evidence: meera logged in on 28 Oct at 03:14:07 from her usual IP 10.0.0.7; all her other logins are between 09:00 and 16:00.
- Harmless explanation: night work or a scheduled task.
- Next steps: confirm with meera and check what the session did.

**F3: Two IPs for one user within minutes (Medium)**
- Evidence: anna logged in from 10.0.0.5 at 14:20:11, then from 192.0.2.77 at 14:26:48 (6 minutes 37 seconds later).
- Harmless explanation: VPN or mobile network.
- Next steps: ask anna, and check whether 192.0.2.77 is a known VPN exit.

## Looked suspicious but is probably fine
ravi failed twice (10:20:02 and 10:20:15) and then succeeded at 10:20:41 from his usual IP during working hours. This is consistent with a mistyped password.

## Recommendations
1. Reset ravi's credentials and review his activity after 11:00:36.
2. Block or rate-limit 198.51.100.23 and alert when one IP fails against several users within a minute.
3. Enforce MFA, especially for remote logins.
4. Alert on logins outside a user's usual hours or from a second IP within a short time.

## Limitations
The log is tiny and synthetic. It has no MFA, location or session data, so nothing above proves compromise; every item is a lead for investigation, not a conclusion.
