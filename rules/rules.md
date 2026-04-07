alert tcp any any -> any any (msg:"Nmap SYN Scan Detected"; flags:S; flow:stateless; detection_filter:track by_src, count 20, seconds 5; sid:1000101; rev:1;) 

alert tcp any any -> any any (msg:"Nmap FIN Scan Detected"; flags:F; flow:stateless; detection_filter:track by_src, count 5, seconds 10; sid:1000101; rev:1;) 

alert tcp any any -> any any (msg:"Nmap Service Scan Behavior"; flow:stateless; detection_filter:track by_src, count 50, seconds 10; sid:1000102; rev:1;) 

alert icmp any any -> any any (msg:"Possible Nmap OS Detection (ICMP)"; itype:8; detection_filter:track by_src, count 5, seconds 5; sid:1000103; rev:1;) 

alert tcp any any -> any 22 (msg:"SSH Brute Force Detected"; flow:to_server; flags:S+; detection_filter:track by_src, count 5, seconds 60; sid:1000201; rev:1;) 

alert http any any -> any any (msg:"SQL Injection Attempt"; flow:to_server; http.uri; content:"or"; nocase; http.uri; content:"="; sid:1000003; rev:1;)

alert tcp any any -> any 4444 (msg:"Possible Reverse Shell Connection"; flow:to_server; sid:1000005; rev:1)
