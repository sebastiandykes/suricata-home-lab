# Setup Guide

## Tools Used
- Suricata (Ubuntu)
- Kali Linux
- Nmap
- Hydra

## Installation

sudo apt update
sudo apt install suricata

## Start Suricata

sudo suricata -c /etc/suricata/suricata.yaml -i enp0s3

## Log Location

/var/log/suricata/eve.json