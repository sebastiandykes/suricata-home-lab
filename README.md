Suricata Home Lab

Overview:

This cybersecurity home lab applies the IDS Tool Suricata to check network traffic with the intent to distinguish regular traffic and false positives from malicious traffic and true positives. Suricata is installed and employed on an Ubuntu Virtual Machine while malicious traffic is generated from a Kali VM. Several tools used from the attacking machine included Nmap, Hydra, and Curl. To detect the scans and intrusion attempts specific rules were designed and included in a local rules file. Threshold rules were also implemented to filter out false positives and unnecessary detections. Lots of errors and issues occurred during the implementation of rules and during the attempts to detect simulated attacks. These were all resolved with troubleshooting and alert tuning to ensure detection remained effective. Each intrusion attempted was successfully detected with an associated alert in the fast logs and json logs.

Example Scans from Kali VM:
 - nmap -sS -A <target-ip>
 - nmap -sF -A <target-ip>
 - hydra -l root -P rockyou.txt -t 4 ssh://<target-ip>
 - curl "http://<target-ip>/login.php?id=%27%20OR%20%271%27%3D%271"

Example Suricata Rules on Ubuntu VM:
  - alert tcp any any -> any any (msg:"Nmap SYN Scan Detected"; flags:S; flow:stateless; detection_filter:track by_src, count 20, seconds 5; sid:1000101; rev:1;) 
  - alert tcp any any -> any any (msg:"Nmap FIN Scan Detected"; flags:F; flow:stateless; detection_filter:track by_src, count 5, seconds 10; sid:1000101; rev:1;) 
  - alert tcp any any -> any 22 (msg:"SSH Brute Force Detected"; flow:to_server; flags:S+; detection_filter:track by_src, count 5, seconds 60; sid:1000201; rev:1;)
  - alert http any any -> any any (msg:"SQL Injection Attempt"; flow:to_server; http.uri; content:"or"; nocase; http.uri; content:"="; sid:1000003; rev:1;)

Example Suricata Threshold Limit on Ubuntu VM:
 - threshold gen_id 1, sig_id 2200121, type limit, track by_src, count 1, seconds 60