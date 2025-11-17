# splunk-bruteforce-project
## Project Overview
This project demonstrates the process of detecting potential brute‑force SSH activity using Splunk. I ingested Linux authentication logs and used SPL keyword searches to identify failed logins, suspicious username attempts, and general authentication patterns that could indicate malicious behavior.

## Tools Used
- Splunk Enterprise (Free vers.)
- Linux authentication log sample
- Basic SPL search queries

## Dataset Summary
The log file included:
- Failed SSH login attempts
- Invalid username attempts
- Multiple authentication events from different sources
- Successful login entries for comparison

## Analysis Steps

### 1. General authentication event search
```
index=main sourcetype=linux_secure "sshd"
```

### 2. Failed login attempts
```
index=main sourcetype=linux_secure "Failed password"
```

### 3. Suspicious or common attack usernames
```
index=main sourcetype=linux_secure ("invalid user" OR "root" OR "admin" OR "oracle")
```

### 4. Successful logins
```
index=main sourcetype=linux_secure "Accepted password"
```

### 5. Pattern Review
I reviewed:
- Frequency of failed logins
- Attempts across multiple usernames
- Sequences of failures followed by a successful login
- Timing and grouping of authentication events

## Findings
The logs showed repeated failed login attempts, username enumeration, and multiple invalid user attempts. These patterns are consistent with early-stage brute‑force behavior, even without extracting an attacker IP.

## Recommendations
- Implement account lockout thresholds
- Restrict SSH access to trusted IP ranges
- Disable unused or default accounts
- Require MFA where possible
- Monitor and alert on repeated failed authentication attempts

## Skills Demonstrated
- SIEM log review in Splunk
- SPL keyword-based searching
- Identification of authentication anomalies
- Documentation of findings and remediation recommendations
