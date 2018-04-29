# Project 9 - Honeypot

Time spent: **10** hours spent in total

> Objective: Setup a honeypot and intercept some attempted attacks in the wild.

## Honeypots Deployed

### Dionaea Sensor
* Dionaea is "meant to be a nepenthes successor, embedding python as scripting language, using libemu to detect shellcodes, supporting ipv6 and tls."

### Conpot Sensor
* Conpot is a "low interactive server side Industrial Control Systems honeypot designed to be easy to deploy, modify and extend."

### Snort Sensor
* Snort is an "open source intrusion prevention system capable of real-time traffic analysis and packet logging."

### Suricata Sensor
* Suricata is "capable of real time intrusion detection (IDS), inline intrusion prevention (IPS), network security monitoring (NSM) and offline pcap processing."

### Kippo Sensor
* Kippo is a medium-interaction SSH honeypot written in Python. Kippo is used to log brute force attacks and the entire shell interaction performed by an attacker.

## Issues Encountered

I encountered issues installing the mhn into my VM at first due to a required site being down (httpbin.org), however that was later remedied when the github repo with the installation was updated.

I also ran into trouble installing the honeypot 'Cowrie', as the installation could not complete due to an error stating that 'setuptools' was not up-to-date and needed version 18.5 or higher. This error is a bug, since 'setuptools' on the VM was version 39. Despite that I recreated the VM, installed the 'setuptools' at version 18.5, and still the same error appeared. I gave up on the installation and instead installed the previous iteration of the honeypot - 'Kippo'.

The same error also appeared for 'Glastopf' where 'setuptools' was not up-to-date.

## Summary of Data

|<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/top5ips.png" width="50%">|<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/top5pots.png" width=50%>|
<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/sensors.png">
<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/payloadssnort.png">
<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/payloadssuricata.png">
<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek9/master/kippotop.png">

## Bonus Objectives


## Notes
