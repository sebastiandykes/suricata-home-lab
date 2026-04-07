# Log Analysis

## Nmap Detection
Observed alerts triggered by Nmap scans indicating reconnaissance activity.

## Brute Force Detection
Multiple SSH login attempts triggered threshold-based alert.

## False Positives
Generic protocol alerts were filtered to reduce noise.

## Alert Tuning 

Encountered repeated alerts (SID 2200121) related to generic protocol decoding. 

Implemented thresholding using: 

 - threshold gen_id 1, sig_id 2200121, type limit, track by_src, count 1, seconds 60 

This reduced alert noise and improved signal-to-noise ratio. 

## Detection Tuning 

Initial rules generated excessive ICMP alerts due to overly broad matching. 

Refined rules to: 

 - detect only ICMP echo requests 

 - implement threshold-based detection for scanning 

 - improve SSH brute force detection with flow direction 

Result: Improved alert accuracy and reduced false positives. 

## Troubleshooting Detection 

Encountered issue where SSH brute force detection was not triggering. 

Root causes: 

Hydra wordlist not found, preventing attack simulation 

ICMP rule generating excessive noise 

Fixes: 

Corrected Hydra command with proper wordlist path 

Disabled overly broad ICMP rule 

Implemented refined SSH detection rule 

Result: Successfully detected brute force attempts in Suricata logs. 

 

## Troubleshooting SSH Detection 

Issue: Hydra brute force attempts failed with "connection refused". 

Root cause: SSH service was not running on the target system. 

Resolution: 

Installed and started OpenSSH server 

Verified port 22 was open 

Adjusted firewall rules 

Result: Successfully generated SSH traffic and triggered Suricata detection alerts. 

## Log Parsing Issue 

Encountered JSON parsing errors when analyzing Suricata eve.json logs using jq. 

Cause: Log file was being written to in real time, resulting in incomplete JSON entries. 

Solution: 

 - Used jq directly on file instead of piping 

 - Implemented error suppression (2>/dev/null) 

 - Used tail -f for real-time monitoring 

Result: Successfully parsed and analyzed alert events. 

 

## Log Monitoring Issue 

Issue: Suricata eve.json logs were not showing current alerts. 

Root causes investigated: 

 - Service status 

 - Network interface configuration 

 - Log file timestamps 

 - Traffic generation 

Resolution: 

 - Restarted Suricata service 

 - Cleared old logs 

 - Verified correct interface monitoring 

 - Generated new traffic for validation 
 
Result: Successfully restored real-time log visibility. 