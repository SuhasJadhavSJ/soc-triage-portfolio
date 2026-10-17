# INC-003: Windows User Account Modification

**Date:** 17 October 2026  
**Endpoint:** SOC-Windows-Endpoint  
**Source:** Wazuh SIEM  
**Severity:** Medium, based on Wazuh Rule Level 8  
**Event ID:** 4738  
**Wazuh Rule ID:** 60110  
**Classification:** Benign True Positive, pending confirmation of the event's relationship to the authorized lab setup

## Summary

Wazuh generated a Level 8 alert after Windows Security recorded a user account modification involving `SOC-LabUser`. The event identifies `windows` as the initiating account. The activity occurred during the setup of a dedicated lab account for authorized SOC investigation exercises.

## Evidence

- Windows Security Event ID: 4738
- Wazuh rule description: User account changed
- Target account: SOC-LabUser
- Initiating account: windows
- Endpoint: SOC-Windows-Endpoint
- Event time: 17 October 2026, 12:56:31 UTC
- MITRE ATT&CK mapping: T1098, Account Manipulation
- No specific changed attribute is identified in the supplied event.

## Investigation and Verdict

The event confirms that Windows audited a user account change. The activity is consistent with authorized lab administration. The event does not, by itself, establish malicious account manipulation or identify an external threat actor.

**Verdict:** Benign True Positive, contingent on confirming the event corresponds to the authorized account setup.

## Recommended Actions

1. Correlate the event with the account-creation and account-change timeline.
2. Review adjacent Security events for account creation, group membership changes, and privilege assignments.
3. Verify that `SOC-LabUser` has only the intended permissions.
4. Retain the event as a benign detection example in the SOC investigation portfolio.
5. Do not suppress the rule globally; account modification alerts remain valuable for detecting unauthorized persistence.

## Closure Criteria

Close the case as benign after confirming that the change was authorized and that no unexpected privilege or group membership changes occurred.