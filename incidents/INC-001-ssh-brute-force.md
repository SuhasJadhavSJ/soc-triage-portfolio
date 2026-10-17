# Incident Report: INC-001 - SSH Brute-Force & Compromise of 'ubuntu' Account

- **Date/Time:** Oct 15, 2026, 16:04:03 IST (10:34:03 UTC)
- **Monitoring Tool:** Wazuh SIEM
- **Alert:** Rule 40112 (Multiple authentication failures followed by a success)[cite: 1]
- **Target System:** SOC-Ubuntu-Server (192.168.56.10)[cite: 1]
- **Target User:** ubuntu[cite: 1]
- **Attacking IP:** 192.168.56.1 (Port 55884)[cite: 1]
- **MITRE Tactics:** T1110 (Brute Force), T1078 (Valid Accounts)

---

### Incident Summary
A high-severity alert triggered on `SOC-Ubuntu-Server` after dozens of failed SSH password attempts ended in a successful login for the `ubuntu` user from IP `192.168.56.1`[cite: 1]. The short timeframe between the failed attempts and the logon points directly to an automated dictionary attack that guessed the account password. I confirmed an active interactive shell on the server, terminated the session, and locked password authentication on the service.

---

### Log Analysis & Timeline
Reviewing the 83 alerts around 16:03–16:04 IST shows a clear sequence of events[cite: 1]:

- **16:03:43 – 16:03:45:** The host logged rapid SSH/PAM authentication failures within milliseconds (Rules 5503, 5760), typical of an automated tool cycling credentials[cite: 4].
- **16:03:45:** Wazuh flagged Rule 5763 after hitting the threshold for an SSH brute-force attack[cite: 4].
- **16:03:49 – 16:03:55:** Failed logon events continued piling up under Rule 2502 and Rule 40111[cite: 1, 2, 3].
- **16:04:03 (Point of Breach):** SSH accepted the password for user `ubuntu` from `192.168.56.1` (Rule 40112)[cite: 1].
- **16:04:03 (+1ms):** PAM opened an interactive session (Rule 5501)[cite: 1].

---

### Host Investigation
I logged into the server console to verify whether the session was still active and check for unauthorized commands:

1. **Active Sessions (`who -u`):**
   Confirmed user `ubuntu` was connected via `pts/0` from `192.168.56.1`.
2. **Activity Inspection:**
   Reviewed `/var/log/auth.log` and checked the shell history (`~/.bash_history`) to see if any reconnaissance commands, privilege escalation attempts, or downloads had taken place before intervention.

---

### Triage Verdict
- **Verdict:** True Positive (Unauthorized Access / Compromised Account)
- **Assessment:** The attacker successfully cracked the credentials for `ubuntu`[cite: 1]. Because `ubuntu` has sudo rights on this machine, immediate containment was necessary to prevent lateral movement or persistence.

---

### Actions Taken & Remediation

1. **Terminated the Attacker's Session:**
   Killed all active processes and shells under the user account:

   sudo pkill -KILL -u ubuntu