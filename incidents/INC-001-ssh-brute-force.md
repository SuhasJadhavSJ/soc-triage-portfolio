# Incident Report : INC-001 Brute Force Attack

**Date/Time:** 2026-10-15T10:34:03.799Z (16:04:03 IST)
**SIEM / Engine:** Wazuh (Alert Level: 12)
**Rule ID:** `40112` — *Multiple authentication failures followed by a success*
**Target Host:** `SOC-Ubuntu-Server` (Agent ID: `001` | IP: `192.168.56.10`)
**Account:** `ubuntu`
**Source IP / Port:** `192.168.56.1` : `55884`
**MITRE ATT&CK Mapping:** T1110 (Brute Force / Password Guessing), T1078 (Valid Accounts)

## 1. Executive Summary
At 10:34:03 UTC, a High Severity (Level 12) rule triggered on host `SOC-Ubuntu-Server` after consecutive SSH authentication failures culminated in a successful password-based login for accoint `ubuntu` originating from intern host `192.168.56.1`. Preliminary log inspection indicated potential brute-force compromise of a default system account. Active session verification and source host quarantine are initiated.

## 2. Multi-Stage Log Correlation & Attack Chain

Correlating the 83 events across `wazuh-alerts-4.x` reconstructs the complete attack timeline[cite: 1]:

| Phase | Timestamp (IST) | Rule ID & Level | Event Signature & Log Details | Analysis / MITRE Mapping |
| :--- | :--- | :--- | :--- | :--- |
| **1. Rapid Probing** | `16:03:43` – `16:03:45`[cite: 4] | `5503` (L5), `5760` (L5)[cite: 4] | `PAM: User login failed` / `sshd: authentication failed`[cite: 4] | High-velocity dictionary spray against port 22[cite: 4]. |
| **2. Aggregation** | `16:03:45.813`[cite: 4] | `5763` (L10)[cite: 4] | `sshd: brute force trying to get access to the system`[cite: 4] | Wazuh correlation detects threshold exceedance[cite: 4]. |
| **3. Continued Guessing** | `16:03:49` – `16:03:55`[cite: 1, 2, 3] | `2502` (L10), `40111` (L10)[cite: 1, 2] | `syslog: User missed the password more than one time`[cite: 1, 2] | Multiple failed attempts in short duration (T1110)[cite: 1, 2]. |
| **4. Credential Match** | `16:04:03.799`[cite: 1] | **`40112` (L12)**[cite: 1] | `Accepted password for ubuntu from 192.168.56.1 port 55884 ssh2`[cite: 1] | Valid credentials guessed; composite rule triggered[cite: 1]. |
| **5. Session Spawn** | `16:04:03.800`[cite: 1] | `5501` (L3)[cite: 1] | `PAM: Login session opened.`[cite: 1] | Interactive shell established 1ms post-auth (T1078)[cite: 1]. |

## 3. Host-Level Forensic Verification

Investigation executed directly on `SOC-Ubuntu-Server` (`192.168.56.10`) yielded the following operational findings:

1. **Active Terminal Sessions (`who -u`):**
   * Identified active session: `ubuntu  pts/0  2026-10-15 16:04 (192.168.56.1)`.
2. **Audit & Command Inspection:**
   * Checked `/var/log/auth.log` and user history (`~/.bash_history`) to monitor for unauthorized execution (`sudo`, reconnaissance scripts, persistence tools).


## 4. Verdict & Impact Assessment

* **Final Verdict:** **True Positive (Confirmed Account Takeover)**
* **Impact Analysis:** An attacker successfully obtained valid credentials for the primary user `ubuntu` via high-frequency automated guessing[cite: 1, 4]. Since the `ubuntu` account possesses default sudo privileges on Ubuntu installations, full host compromise and privilege escalation are likely if left uncontained.

## 5. Containment & Remediation Actions Taken

1. **Active Session Severance:**
   * Terminated rogue interactive sessions on `SOC-Ubuntu-Server`:
     sudo pkill -KILL -u ubuntu

2. **Account Restriction:**
   * Locked user password to prevent persistent logon:
     sudo passwd -l ubuntu

3. **Hardening & Service Defense:**
   * Disabled SSH password authentication in `/etc/ssh/sshd_config`:
     PasswordAuthentication no
     PermitRootLogin no
     PubkeyAuthentication yes

   * Applied configuration: `sudo systemctl restart sshd`.
4. **Detection Engineering / Active Response:**
   * Configured Wazuh Active Response on the manager to execute `firewall-drop` / `iptables` for 3600 seconds on any source IP triggering Rule `5763` or `40112`[cite: 1, 4].