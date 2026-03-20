

## Simulated Attack: Successful SSH Login

After generating multiple failed SSH login attempts, a successful SSH login was performed using valid credentials.

Purpose:
Simulate a scenario in which an attacker eventually gains access after repeated failed attempts.

![image](screenshots/successful-ssh-login.png)

## Detection: Successful SSH Logins

Analyzed authentication logs to identify successful SSH login activity.

Query:

index=main "Accepted password"

This search returns successful SSH authentication events recorded in the authentication log.

![image](screenshots/successful-logins-search.png)

## Detection: Successful SSH Logins by Source IP

Used regex extraction to identify the source IP address associated with successful SSH logins.

Query:

index=main "Accepted password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort -count

This helps identify which hosts successfully authenticated to the system.

## Detection Logic

A potentially suspicious authentication pattern is identified when:

- Multiple failed login attempts are followed by a successful login
- The events originate from the same source IP
- The activity occurs within a short period of time

This pattern may indicate a successful brute-force attempt or unauthorized access using valid credentials.

This logic can be used in a SIEM to prioritize investigation and generate alerts for possible account compromise.

## Insight

This detection improves visibility into authentication behavior by showing not only failed access attempts, but also whether access was eventually gained.

In a real-world SOC environment, correlating failed and successful logins from the same source can help analysts identify compromised accounts and investigate possible intrusion activity more effectively.
