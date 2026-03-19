## Splunk Installation

Installed Splunk using dpkg package manager.
Resolved dependencies using apt if required.

## Splunk Service Start

Successfully started Splunk service.

System completed all preliminary checks and launched the web interface on port 8000.

Splunk is now operational and ready for use.


## Issue: No Admin User Created

### Problem
Splunk started successfully but displayed:
"No users exist. Please set up a user."

### Resolution

Stopped Splunk service:
```bash
sudo /opt/splunk/bin/splunk stop
```
Created user seed configuration file:
```
sudo nano /opt/splunk/etc/system/local/user-seed.conf
```
Added the following configuration:
> [!NOTE]
> [user_info]
> USERNAME = admin
> PASSWORD = <redacted>

Finally, Restarted splunk
sudo /opt/splunk/bin/splunk start --accept-license --answer-yes --run-as-root

Outcome
Successfully created admin user and gained access to Splunk web interface.
